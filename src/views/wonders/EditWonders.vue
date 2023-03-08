<script setup>
import axios from "axios";
import { reactive, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";
 
let wonderToUpdate = reactive({
  id: 0,
  name: "",
  location: "",
  imageUrl: "",
});
 
const router = useRouter();
const route = useRoute();
 
onMounted(() => {
  axios
    .get(`http://localhost:3000/wonders/${route.params.id}`)
    .then((response) => {
      wonderToUpdate.id = response.data.id;
      wonderToUpdate.name = response.data.name;
      wonderToUpdate.location = response.data.location;
      wonderToUpdate.imageUrl = response.data.imageUrl;
    });
});
 
const updateWonder = () => {
  axios.put(`http://localhost:3000/wonders/${route.params.id}`, wonderToUpdate).then(() => {
    router.push("/");
  });
};
</script>
<template>
  <div class="container mt-4 w-50">
    <form @submit.prevent="updateWonder">
      <legend>Update Wonders</legend>
      <div class="mb-3">
        <label for="txtWonderName" class="form-label">Name</label>
        <input
          type="text"
          v-model="wonderToUpdate.name"
          class="form-control"
          id="txtWonderName"
        />
      </div>
      <div class="mb-3">
        <label for="txtLocation" class="form-label">Location</label>
        <input
          type="text"
          v-model="wonderToUpdate.location"
          class="form-control"
          id="txtLocation"
        />
      </div>
      <div class="mb-3">
        <label for="txtImageUrl" class="form-label">Image URL</label>
        <input
          type="text"
          v-model="wonderToUpdate.imageUrl"
          class="form-control"
          id="txtImageUrl"
        />
      </div>
      <button type="submit" class="btn btn-primary">Update</button>
    </form>
  </div>
</template>