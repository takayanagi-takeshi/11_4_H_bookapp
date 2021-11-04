<template>
  <div id="app">
    <div>
      書籍名：
      <input type="text" v-model="searchbox">
      <button @click="search">検索する</button>
    </div>
    <div>
      著者名：
      <input type="text" v-model="searchbox2">
      <button @click="search2">検索する</button>
      <ul>
        <li v-for="book in books" :key="book.id">
          <img :src="book.volumeInfo.imageLinks.smallThumbnail" alt="">
          {{book.volumeInfo.title}}
          {{book.volumeInfo.authors[0]}}
        </li>
      </ul>      <!-- <ul>
        <li v-for="author in authors" :key="author.id">
          <img :src="book.volumeInfo.imageLinks.smallThumbnail" alt="">
          {{book.volumeInfo.title}}

        </li>
      </ul> -->
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      books: '',
      searchbox: '',
      orderBy: 'newest',
      maxResults: '10',
      searchbox2: '',
      authors: '',
    }
  },
  computed: {

  },
  methods: {
    search() {
      axios.get(
          `https://www.googleapis.com/books/v1/volumes?q=intitle:${this.searchbox}&orderBy=${this.orderBy}&maxResults=${this.maxResults}`
        )
        .then(response => {
          console.log(response.data.items)
          this.books = response.data.items 
        })
    },
    search2() {
      axios.get(
          `https://www.googleapis.com/books/v1/volumes?q=inauthor:${this.searchbox2}`
        )
        .then(response => {
          console.log(response.data.items)
          this.books = response.data.items 
        })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
