<template>
  <div>
    <h2 class="userListTD">User List:</h2>
    <table class="userTable">
      <tr>
        <td><strong>id</strong></td>
        <td>Name</td>
        <td>Surname</td>
        <td>Email</td>
        <td>Avatar</td>
      </tr>
      <br />
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.first_name }}</td>
        <td>{{ item.last_name }}</td>
        <td>{{ item.email }}</td>

        <img :src="item.avatar" />

        <td>
          <v-btn @click="deleteUser(item.id)">DELETE</v-btn>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UserList",
  data() {
    return {
      list: {},
    };
  },
  methods: {
    async getData() {
      await axios.get("https://reqres.in/api/users/").then((resp) => {
        this.list = resp.data.data;
      });
    },
    async deleteUser(userID) {
      await axios
        .delete("https://reqres.in/api/users?page=2" + userID)
        .then(() => {
          let i = this.list.map((data) => data.id).indexOf(userID);
          this.list.splice(i, 1);
          console.log("user deleted");
        });
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
input[type="text"] {
  background-color: #ebe6e6;
  width: 15%;
  height: 12%;
  border: black 2px;
}
</style>
