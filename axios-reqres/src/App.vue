<template>
  <div>
    <h1>Getting data from Reqres API</h1>
    <table>
      <td><UserList /></td> <br> <br>
      <td><AddUser /></td>
    </table>
  </div>
</template>

<script>
import UserList from '@/components/Users.vue'
import AddUser from './components/AddUser.vue'
export default {
  name: 'App',
  components:{
    UserList,
    AddUser
}
} 
</script>

<style>

</style>