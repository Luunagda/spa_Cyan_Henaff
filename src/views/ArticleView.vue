<template>
  <div class="article">
    <h1>This is an about page</h1>
    <Article msg="Welcome to Your Vue.js App"/>
    
  </div>

</template>
<script>
import Article from '@/components/Article.vue'

 export default {
  name: 'Article',
  components: {
    Article
  }
 }
</script>