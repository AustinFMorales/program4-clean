<template>
  <h1>Program 4: Website + Storage</h1>
  <Button text="Load Data" color="blue"></Button>
  <Button text="Clear Data" color="red"></Button>
  <QueryForm/>
  <Button text="Query" color="green"></Button>
</template>

<script>
import Button from  './components/Button.vue'
import QueryForm from './components/QueryForm.vue'
const {BlobServiceClient} = require('@azure/storage-blob');
const {DefaultAzureCredential} = require('@azure/identity')

export default {
  name: 'App',
  components: {
    Button,
    QueryForm
  },
  data() {
    return {
      // to store query results from cosmos DB
      query_results: [],
      // hard code the url - the professor will change the data 
      blob_url: 'https://css490.blob.core.windows.net/lab4/input.txt',
      my_blob_url: 'https://arrowman67.blob.core.windows.net/databank'

    }
  },
  methods : {    
    // responsible for loading data from hard-coded blob url
    // to destination blob url - my_blob_url 
    loadData() {
      // blob service client essentially is the top object in SDK
      // JS does not like used unused variables so there will be a lot of bloat
      const defaultAzureCredential = new DefaultAzureCredential();

      const myServiceClient = new BlobServiceClient(this.my_blob_url, defaultAzureCredential);
      
      // this will not work, only placeholder atm
      // need to parse the container name, and the blob name
      this.copyBlob(myServiceClient, this.blob_url, this.blob_url, this.my_blob_url, this.my_blob_url);
      
    },
    
    // copy blob method - from azure documentation 
    // sourceblobcontainer and destinationBlobContainer = container names 
    // sourceblobName and destinationBlobName = blob file name
    async copyBlob(blobServiceClient, sourceBlobContainer, sourceBlobName, destinationBlobContainer, destinationBlobName) {
      // create container clients
      const sourceContainerClient = blobServiceClient.getContainerClient(sourceBlobContainer);
      const destinationContainerClient = blobServiceClient.getContainerClient(destinationBlobContainer);

      // create blob clients
      const sourceBlobClient = await sourceContainerClient.getBlobClient(sourceBlobName);
      const destinationBlobClient = await destinationContainerClient.getBlobClient(destinationBlobName);

      // start the copy
      const copyPoller = await destinationBlobClient.getBlobClient(sourceBlobClient.url);
      console.log('starting copy from A to B');

      //wait until done
      await copyPoller.pollUntilDone();

    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

</style>
