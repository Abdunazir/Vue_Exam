<template>
  <div class="asos">
    <div class="container">
      <products ref="products_modal" />
      <div class="">
        <button class="btn w-100 btn-success mt-3" @click="createItem">
          Create Product
        </button>
      </div>
      <div class="row ">
        <div class="col-4 my-2" v-for="(item, index) in items" :key="index">
          <div class="card py-2">
            <div class="card-head">
              <h3 class="text-center mt-2">Products</h3>
            </div>
            <div class="card-body">
              <h6>Brand: {{ item.brand }}</h6>
              <h6>Group: {{ item.group }}</h6>
              <h6>Name: {{ item.name }}</h6>
              <h6>Price: {{ item.price }}</h6>
              <h6>Arrival price: {{ item.arrival_price }}</h6>
              <h6>Selling price: {{ item.selling_price }}</h6>
              <h6>Description: {{ item.description }}</h6>
            </div>
            <div class="card-foot d-flex justify-content-between px-2">
              <button class="btn btn-info bb border-0 text-light" @click="editItem(item)">
                Edit
              </button>
              <button class="btn btn-danger " @click="deleteItem(item._id)">
                Delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import products from "@/components/pages/products";
  import Notification from "@/plugins/Notification";
  import http from "@/plugins/api";
  import axios from "axios";
  import { ref } from "vue";
  const items = ref([]);
  const products_modal = ref();

  const getProducts = () => {
    http
      .get("/api/products")
      .then((res) => {
        items.value = res.data.products;
        console.log(res.data.products);
      })
      .catch((error) => {
        console.log(error);
      });
  };

  const deleteItem = (item) => {
    products_modal.value.openModal(item);
  };

  const createItem = () => {
    products_modal.value.openModal();
  };

  const editItem = (item) => {
    products_modal.value.openModal(item);
  };

  const logOut = () => {
    localStorage.removeItem("token");
    localStorage.removeItem("roles");
    location.reload();
  };
  getProducts();
</script>

<style lang="scss" scoped>
// .left{
//   background: #1A1A2E;
//   height: 100vh;
// }
.asos{
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
