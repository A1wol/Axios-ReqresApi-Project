<template>
  <div>
    <div class="container">
      <h2 class="text-center">Add New User</h2>
      <div class="row">
        <div class="col-md-12">
          <div>
            <label>First Name</label>
            <v-text-field v-model="newItem.first_name" />
          </div>
          <div>
            <label>Last name</label>
            <v-text-field
              rows="5"
              class="form-control"
              v-model="newItem.last_name"
            />
          </div>
          <div>
            <label>Email</label>
            <v-text-field class="form-control" v-model="newItem.email" />
          </div>
          <v-btn class="btn btn-primary" @click="addUser()">Create</v-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AddUser",
  data() {
    return {
      list: [],
      newItem: {
        first_name: "",
        last_name: "",
        email: "",
      },
      baseURL: "https://reqres.in/api/users/",
    };
  },
  methods: {
    async getData() {
      await axios.get(this.baseURL).then((resp) => {
        this.list = resp.data.data;
      });
    },
    async addUser() {
      await axios
        .post(this.baseURL, {
          id: Date.now(),
          first_name: this.newItem.first_name,
          last_name: this.newItem.last_name,
          email: this.newItem.email,
        })
        .then((resp) => {
          console.log(
            "added: " + resp.data.first_name + " " + resp.data.last_name
          );
          this.list.push(this.newItem);
          console.log(this.list);
          (this.newItem.first_name = ""),
            (this.newItem.last_name = ""),
            (this.newItem.email = "");
        })
        .catch((error) => console.log(error));
    },
  },
  created() {
    this.getData();
  },
};
</script>

<style></style>
