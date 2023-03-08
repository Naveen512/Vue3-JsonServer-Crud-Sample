<script setup>
import axios from "axios";
import { reactive } from "vue";
import { useRouter } from "vue-router";
let newWonder = reactive({
  name: "",
  location: "",
  imageUrl: "",
});
const router = useRouter();
const addNewWonder = () => {
  axios.post("http://localhost:3000/wonders", newWonder).then(() => {
    router.push("/");
  });
};
</script>

<template>
  <div class="container mt-4 w-50">
    <form @submit.prevent="addNewWonder">
      <legend >Add New Wonder's</legend>
      <div class="mb-3">
        <label for="txtwonderName" class="form-label">Wonder Name</label>
        <input
          type="text"
          v-model="newWonder.name"
          class="form-control"
          id="txtwonderName"
        />
      </div>
      <div class="mb-3">
        <label for="txtLocation" class="form-label">Location</label>
        <input
          type="text"
          v-model="newWonder.location"
          class="form-control"
          id="txtLocation"
        />
      </div>
      <div class="mb-3">
        <label for="txtImageUrl" class="form-label">Image URL</label>
        <input
          type="text"
          v-model="newWonder.imageUrl"
          class="form-control"
          id="txtImageUrl"
        />
      </div>
      <button type="submit" class="btn btn-primary">Add</button>
    </form>
  </div>
</template>
