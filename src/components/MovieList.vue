<template>
    <form class="Search-form">
      <input class="Search-input" type="text" v-model="searchKeyword" @input="searchMovie" placeholder="Search movie...">
    </form>

    <div class="Movie-list">
      <div class="Movie-wrapper" v-if="data" v-for="item in data">
        <img :src="`https://image.tmdb.org/t/p/w500/${item.poster_path}`"/>
        <div class="Movie-info">
          <div class="Movie-title">{{ item.title }}</div>
          <div class="Movie-date">{{ item.release_date }}</div>
          <div class="Movie-rate">{{ item.vote_average }}</div>
        </div>
      </div>
    </div>

  </template>
  
  <script>
  import axios from 'axios'
  export default {
  name: 'MyComponent',
  data () {
    return {
      data: null,
      searchKeyword: ''
    }
  },
  computed: {
    filteredData() {
      return this.data.filter(item => item.title.toLowerCase().includes(this.searchKeyword.toLowerCase()))
    }
  },
  created () {
    axios.get(`${process.env.VUE_APP_BASE_URL}/movie/popular?api_key=${process.env.VUE_APP_API_KEY}`)
      .then(response => (this.data = response.data.results))
  },
  methods: {
    searchMovie() {
      if (this.searchKeyword.length > 5) {
        // Filter data sesuai dengan keyword
        let url = `${process.env.VUE_APP_BASE_URL}/search/movie?query&api_key=${process.env.VUE_APP_API_KEY}&query=${this.searchKeyword}`
        axios.get(url)
        .then(response => {
            this.data = response.data.results
        })
      }
    }
  }
}
  
  </script>
  
<style scoped>
.Search-form {
    width: 75%;
    display: flex;
    align-items: center;
}
.Search-input {
    padding: 10px;
    /* border: none; */
    font-size: 1.2em;
    flex: 1;
}

.Movie-list {
    display: flex;
    flex-wrap: wrap;
  }
.Movie-wrapper {
    flex: 1 0 300px;
    margin: 10px;
    position: relative;
}
.Movie-wrapper img {
    width: 100%;
    height: auto;
}
.Movie-info {
    position: absolute;
    bottom: 0;
    background: rgba(0, 0, 0, 0.7);
    color: #fff;
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
}
.Movie-title {
    font-size: 1.2em;
    font-weight: bold;
    margin-bottom: 5px;
}
.Movie-date, .Movie-rate {
    font-size: 0.8em;
}
</style>