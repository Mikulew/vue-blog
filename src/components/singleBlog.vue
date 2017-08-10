<template>
  <div id="single-blog">
    <h1>{{blog.title}}</h1>
    <article>{{blog.content}}</article>
    <div class="single-blog-wrapper">
      <p class="single-blog-author">Author: {{ blog.author }}</p>
      <p class="single-blog-categories">Categories:</p>
      <ul>
          <li v-for="category in blog.categories">{{ category }}</li>
      </ul>
      <router-link v-bind:to="'/'">
        <button class="single-blog-button">Powrót</button>
      </router-link>

    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    }
  },
  created() {
    this.$http.get('https://vue-blog-8438a.firebaseio.com/posts/' + this.id + '.json')
      .then((data) => data.json())
      .then((data) => this.blog = data)
  }
}

</script>

<style scoped>
  article {
    margin-top: 20px;
  }
  #single-blog {
    max-width: 960px;
    margin: 0 auto;
  }
  .single-blog-wrapper {
    display: flex;
    border: 1px solid #eee;
    padding: 10px;
    margin-top: 20px;
  }
  .single-blog-categories {
    margin: 10px 5px;
  }
  .single-blog-author {
    margin: 10px;
  }
  .single-blog-button {
    margin: 10px;
    padding: 0 10px;
  }
  ul {
    display: inline-flex;
    margin: 10px 0;
  }
  li {
    list-style-type: none;
  }
</style>
