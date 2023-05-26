<script setup>

  import { ref, reactive } from 'vue';

  const collection = reactive([
    {
      id: 1,
      author: "J.R.R. Tolkien",
      title: "Lord of the Rings"
    },
    {
      id: 2,
      author: "J.K. Rowling",
      title: "Harry Potter"
    },
    {
      id: 3,
      author: "Andrzej Sapkowski",
      title: "The Witcher"
    }
  ])
  const wishlist = reactive([])

</script>

<template>
  <h1 class="header">My bookshelft</h1>
  <div class="section">
    <div class="left">
      <div class="collection">
        <h2>Books in collection</h2>

        <ul class="books">
          <li v-for="item in collection" :key="item.id" class="book">
            <p class="number">{{ item.id }}</p>
            <p class="author">{{ item.author }}</p>
            <p class="title">{{ item.title }}</p>
          </li>
        </ul>

      </div>
      <div class="wishlist">
        <h2>My wishlist</h2>
      </div>
    </div>
    <div class="right">asd</div>
  </div>
</template>

<style scoped>

  .header {
    text-align: center;
    padding: 20px 0px;
  }

  .section {
    display: flex;
  }

  .left {
    flex: 1;
    border: 1px solid grey;
  }

  .collection {
    padding: 20px;
  }

  .wishlist {
    padding: 20px;
  }

  .right {
    flex: 1;
    border: 1px solid grey;
  }

</style>
