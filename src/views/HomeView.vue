<template>
  <div class="home">
    
    <h1>Vos articles</h1>
    <div class="article" v-for="article in articles" :key="article.id">
      <a class="card-container">
        <div class="lettre" :style="{ backgroundColor: circleColor }">{{ getFirstletter(article.title) }}</div>
        <h2>{{ article.title }}</h2>
      </a>
    </div>
    
    
  </div>
</template>
<style>
.article {
  display: flex;
  flex-direction: row;

  
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

import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  
  name: 'HomeView',
  components: {
    HelloWorld
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
    generateRandomColor() {
      const randomColor = '#' + Math.floor(Math.random()*16777215).toString(16);
      this.circleColor = randomColor;
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
    }),
    this.generateRandomColor();
  }
}

</script>
