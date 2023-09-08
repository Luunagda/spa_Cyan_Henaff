<template>
  <div class="home">
    
    <h1>Vos articles</h1>
    <div class="article" v-for="article in articles" :key="article.id">
      <a class="card-container">
        <div class="lettre" :style="{ backgroundColor: getRandomColor() }">{{ getFirstletter(article.title) }}</div>
        <h2>{{ article.title }}</h2>
      </a>
    </div>
    
    
  </div>
</template>
<style>
.article {
  padding: 0 2rem;
  margin: 0 auto;
  max-width: 1000px;
}
.card-container {
  display: flex;
  justify-content: left;
  align-items: center;
  text-decoration: none;
  color: #000;
  margin: 1rem 0;
  cursor: pointer;
}
.lettre{
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  color: white;
  margin: 10px;
}
</style>
<script>
// @ is an alias to /src

import Article from '@/components/Article.vue'
import axios from 'axios'

export default {
  
  name: 'Article',
  components: {
    Article
  },
  data() {
    return {
      articles: []
    }
  },
  methods: {
    getFirstletter(title) {
      return title.charAt(0)
    },
    getRandomColor() {
      return '#' + Math.floor(Math.random()*16777215).toString(16);
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/posts')
    .then(response => {
      console.log(response.data)
      this.articles = response.data

    })
    .catch(error => {
      console.log(error)
    })
  }
}

</script>
