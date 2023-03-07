<template>
    <br/>
    <label>First Name</label>
    <br/>
    <input type="text" placeholder="enter first name" v-model="this.first_name"/>
    <br/>
    <label>Last Name</label>
    <br/>
    <input type="text" placeholder="enter last name" v-model="this.last_name"/>
    <br/>
</template>

<script>
export default {
    name: 'query-form',
    data() {
        return {
            first_name: '',
            last_name: ''
        }  
    },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>