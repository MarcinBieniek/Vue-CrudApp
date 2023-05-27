<script setup>
import { ref, defineProps } from 'vue';

const shelfType = ref("collection");
const newName = ref("");
const newTitle = ref("");
const newState = ref("new");

</script>

<template>
  <form @submit.prevent="$emit('addProps', shelfType.value, newName.value, newTitle.value, newState.value)">

    <label>Choose shelf</label>
    <select
      v-model.lazy="shelfType"
      placeholder="Choose one"
    >
      <option value="collection">Collection</option>
      <option value="wishlist">Wishlist</option>
    </select>

    <label>Author name</label>
    <input
      type="text"
      v-model.lazy="newName"
      placeholder="Add name"
    />

    <label>Book title</label>
    <input
      type="text"
      v-model.lazy="newTitle"
      placeholder="Add title"
    />

    <label>New or used?</label>
    <select
      v-model.lazy="newState"
      placeholder="Choose one"
    >
      <option value="new">New</option>
      <option value="used">Used</option>
    </select>

    <button type="submit">Add new item</button>
  </form>
</template>

<style>

</style>