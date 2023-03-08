<script setup>
import { ref, onMounted } from "vue";
import ConfirmDeletePopup from "../../components/ConfirmDeletePopup.vue";
import axios from "axios";
const allWonders = ref([]);
const itemToDeleteId = ref([0]);
let deleteModal;

onMounted(() => {
  deleteModal = new window.bootstrap.Modal(
    document.getElementById("deleteModal"));

  axios.get("http://localhost:3000/wonders").then((response) => {
    allWonders.value = response.data;
  });
});

const openDeleteModal = (id) => {
  itemToDeleteId.value = id;
  deleteModal.show();
};

const confirmDelete = () => {
  axios
    .delete(`http://localhost:3000/wonders/${itemToDeleteId.value}`)
    .then(() => {
      allWonders.value = allWonders.value.filter(
        (_) => _.id !== itemToDeleteId.value
      );
      itemToDeleteId.value = 0;
      deleteModal.hide();
    });
};
</script>
<template>
  <div class="container mt-3">
    <div class="row m-2">
      <div class="col col-md-4 offset-md-4">
        <RouterLink to="/add-wonder" class="btn btn-primary">Add</RouterLink>
      </div>
    </div>
    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div class="col" v-for="item in allWonders" :key="item.id">
        <div class="card">
          <img :src="item.imageUrl" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ item.name }}</h5>
            <p class="card-text">Location: {{ item.location }}</p>
            <router-link class="btn btn-primary" :to="`/edit-wonder/${item.id}`"
              >Edit</router-link
            > | 
            <button
              type="button"
              @click="openDeleteModal(item.id)"
              class="btn btn-danger"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <ConfirmDeletePopup @confirmdelete-click="confirmDelete"></ConfirmDeletePopup>
</template>
