<template>
  <div class="bg-war">
    <div class=" container">
      <users ref="users_modal" />
      <div class="">
        <div class="d-flex justify-content-around">
          <button class="btn btn-success w-100 mt-3" @click="createItem">
            Create Users
          </button>
        </div>
        <div class="row ">
          <div class="col-4 my-2" v-for="(item, index) in items" :key="index">
            <div class="card py-2">
              <div class="card-head">
                <h3 class="text-center mt-2">Users</h3>
              </div>
              <div class="card-body ">
                <h6>Name: {{ item.name }}</h6>
                <h6>Surname: {{ item.surname }}</h6>
                <h6>Age: {{ item.age }}</h6>
                <h6>IsDiploma: {{ item.is_diploma }}</h6>
                <h6>Address: {{ item.address }}</h6>
              </div>
              <div class="card-foot d-flex justify-content-between px-2">
                <button class="btn w-40 bb text-light " @click="editItem(item)">
                  Edit
                </button>
                <button class="btn ml-2 w-40 btn-danger " @click="deleteItem(item._id)">
                  Delete
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import users from "@/components/pages/users";
  import Notification from "@/plugins/Notification";
  import http from "@/plugins/api";
  import axios from "axios";
  import { ref } from "vue";
  const items = ref([]);
  const users_modal = ref();

  const getUsers = () => {
    http
      .get("/api/users")
      .then((res) => {
        items.value = res.data.users;
        console.log(res.data.users);
      })
      .catch((error) => {
        console.log(error);
      });
  };

  const deleteItem = (item) => {
    users_modal.value.openModal(item);
  };

  const createItem = () => {
    users_modal.value.openModal();
  };

  const editItem = (item) => {
    users_modal.value.openModal(item);
  };

 
  getUsers();
</script>

<style lang="scss" scoped>
.bg-war{
  background: #1A1A2E;
}

.card{
  color: rgba(255, 255, 255, 0.70);
  border-radius: 10px;
background: rgba(86, 86, 103, 0.29);
box-shadow: 0px -5px 60px 0px rgba(0, 0, 0, 0.50);
}

.btn{
  width: 45%;
}

.bb{
  background: #13294C;
}
</style>
