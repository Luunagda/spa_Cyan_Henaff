<template>
  <div class="home">
    <h1>Vos articles</h1>
    <div class="article" v-for="article in articles" :key="article.id">
      <a class="card-container" @click="toggleArticleDetails(article.id)">
        <div class="lettre" :style="{ backgroundColor: getRandomColor() }">{{ getFirstLetter(article.title) }}</div>
        <h2>{{ article.title }}</h2>
      </a>
      <!-- Afficher les détails de l'article sélectionné -->
      <div v-if="selectedArticle && selectedArticle.id === article.id">
        <p>{{ selectedArticle.body }}</p>
        <h3>Commentaires:</h3>
        <div v-for="comment in selectedArticleComments" :key="comment.id">
          <h2>{{ comment.name }}</h2>
          <a :href="'mailto:' + comment.email">{{ comment.email }}</a>
          <p>{{ comment.body }}</p>
        </div>
      </div>
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
import axios from 'axios';

export default {
  name: 'Article',
  data() {
    return {
      articles: [],
      selectedArticle: null, // Pour stocker l'article sélectionné
      selectedArticleComments: [], // Initialisation du tableau de commentaires
    };
  },
  methods: {
    getFirstLetter(title) {
      return title.charAt(0);
    },
    getRandomColor() {
      return '#' + Math.floor(Math.random() * 16777215).toString(16);
    },
    toggleArticleDetails(articleId) {
      // Si le lien actuellement sélectionné est le même que celui que vous avez cliqué,
      // réinitialisez selectedArticle pour fermer les informations supplémentaires
      if (this.selectedArticle && this.selectedArticle.id === articleId) {
        this.selectedArticle = null;
        this.selectedArticleComments = [];
      } else {
        // Sinon, chargez les détails de l'article et les commentaires en fonction de l'ID de l'article
        axios.get(`https://jsonplaceholder.typicode.com/posts/${articleId}`)
          .then((response) => {
            this.selectedArticle = response.data;
            // Chargez les commentaires de l'article
            axios.get(`https://jsonplaceholder.typicode.com/posts/${articleId}/comments`)
              .then((commentsResponse) => {
                console.log(commentsResponse.data);
                this.selectedArticleComments = commentsResponse.data;
              })
              .catch((error) => {
                console.log(error);
              });
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((response) => {
        console.log(response.data);
        this.articles = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
