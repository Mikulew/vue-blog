<template>
  <div id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" placeholder="search blogs" v-model="search">
    <div v-for="blog in filteredBlogs" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id">
        <h2>{{blog.title}}</h2>
      </router-link>
      <article>{{blog.content | snippet}}</article>
    </div>
  </div>
</template>

<script>

import searchMixin from '../mixins/searchMixin'

export default {
  data () {
    return {
      blogs: [],
      search: ''
    }
  },
  methods: {

  },
  created() {
    this.$http.get('https://vue-blog-8438a.firebaseio.com/posts.json')
      .then((data) => {
        return data.json();
      })
      .then((data) => {
        let blogsArray = [];
        for (let key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      })
  },
  mixins: [searchMixin]
}
</script>

<style scoped>
  #show-blogs {
    max-width: 800px;
    margin: 0 auto;
  }
  #show-blogs a {
    color: #444;
    text-decoration: none;
  }
  #show-blogs a:hover {
    color: #f99;
    text-decoration: none;
  }
  .single-blog {
    padding: 20px;
    margin: 20px 0;
    background: #eee;
  }
  input[type="text"] {
    width: 100%;
    padding: 6px 0;
    text-indent: 8px;
    margin-top: 10px;
  }
</style>
