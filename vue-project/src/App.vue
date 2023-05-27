<script setup>

  import { ref, reactive } from 'vue';

  const collection = reactive([
    {
      id: 1,
      author: "J.R.R. Tolkien",
      title: "Lord of the Rings",
      state: "new"
    },
    {
      id: 2,
      author: "J.K. Rowling",
      title: "Harry Potter",
      state: " used"
    },
    {
      id: 3,
      author: "Andrzej Sapkowski",
      title: "The Witcher",
      state: "new"
    }
  ])
  const wishlist = reactive([])

  const shelfType = ref("collection")
  const newName = ref("")
  const newTitle = ref("")
  const newState = ref("new")

  const addBook = () => {

    if (shelfType.value == "collection") {

    collection.push(
      {
        id: collection.length + 1,
        author: newName.value,
        title: newTitle.value,
        state: newState.value
      }
    )
    newName.value = ("")
    newTitle.value = ("")

    } else {
      wishlist.push(
        {
          id: wishlist.length + 1,
          author: newName.value,
          title: newTitle.value,
          state: newState.value
        }
      )
      newName.value = ("")
      newTitle.value = ("")
    }
  }

  const deleteBook = (id) => {
    collection.splice(collection.findIndex(item => item.id === id), 1);
  }

  /*const editBook = (id, author, title, state) => {
    const book = collection.find(item => item.id === id);
    if (book) {
      book.author = author;
      book.title = title;
      book.state = state;
    }
  };*/

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
            <p class="state">{{ item.state }}</p>
            <button
              @click="editBook"
              class="button-edit">Edit</button>
            <button
              @click="deleteBook(item.id)"
              class="button-delete">X</button>
          </li>
        </ul>

      </div>
      <div class="wishlist">

        <h2>My wishlist</h2>

        <p v-if="!wishlist.length">Wishlist is empty</p>

        <ul v-else class="books">
          <li v-for="{id, author, title, state} in wishlist" :key="id" class="book">
            <p class="number">{{ id }}</p>
            <p class="author">{{ author }}</p>
            <p class="title">{{ title }}</p>
            <p class="state">{{ state }}</p>
            <button
              @click="editBook"
              class="button-edit">Edit</button>
            <button
              @click="deleteBook(id)"
              class="button-delete">X</button>
          </li>
        </ul>

      </div>
    </div>
    <div class="right">

      <h2>Add new book</h2>

      <form @submit.prevent="addBook">

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

    </div>
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
    margin-right: 10px;
  }

  .collection {
    padding: 20px;
  }

  .book {
    display: flex;
    cursor: pointer;
    justify-content: center;
    align-items: center;
  }

  .number {
    flex: 1;
  }

  .author {
    flex: 4;
  }

  .title {
    flex: 4;
  }

  .state {
    flex: 1;
  }

  .button-delete, .button-edit {
    flex: 1;
    width: 20px;
    margin-right: 5px;
  }

  .wishlist {
    padding: 20px;
  }

  .right {
    flex: 1;
    border: 1px solid grey;
    margin-left: 10px;
    padding: 20px;
  }

  form {
    display: flex;
    flex-direction: column;
  }

  input, select {
    margin-bottom: 10px;
  }

  button {
    margin: 10px 0px;
    width: 50%;
  }

</style>
