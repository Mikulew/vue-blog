<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted">
      <label for="blog-title">Blog Title: </label>
      <input id="blog-title" type="text" required v-model.lazy="blog.title">
      <label for="blog-content">Blog Content</label>
      <textarea id="blog-content" name="name" rows="8" cols="80" v-model.lazy="blog.content"></textarea>
      <div id="checkboxes">
        <label>Lifestyle</label>
        <input type="checkbox" name="" value="lifestyle" v-model="blog.categories">
        <label>Weather</label>
        <input type="checkbox" name="" value="weather" v-model="blog.categories">
        <label>Politics</label>
        <input type="checkbox" name="" value="politics" v-model="blog.categories">
        <label>Events</label>
        <input type="checkbox" name="" value="events" v-model="blog.categories">
        <label>Sport</label>
        <input type="checkbox" name="" value="sport" v-model="blog.categories">
      </div>
      <label for="blog-select">Author: </label>
      <select id="blog-select" v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button v-on:click.prevent="post">Add Blog</button>
    </form>
    <div v-if="submitted">
      <h3>Thanks for adding your post!</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog title: {{blog.title}}</p>
      <p>Blog content: </p>
      <p>{{blog.content}}</p>
      <p>Blog Categories: </p>
      <ul>
        <li v-for="category in blog.categories">{{category}}</li>
      </ul>
      <p>Author: {{blog.author}}</p>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ["John Smith", "Jack Sparrow", "Neo Number One", "Sam Unplagged", "Richard Heartmaker"],
      submitted: false
    }
  },
  methods: {
    post: function() {
      this.$http.post('https://vue-blog-8438a.firebaseio.com/posts.json', this.blog)
        .then((data) => {
          console.log(data);
          this.submitted = true;
      });
    }
  }
}
</script>

<style>
  #add-blog * {
    box-sizing: border-box;
  }
  #add-blog {
    margin: 20px auto;
    max-width: 500px;
  }
  label {
    display: block;
    margin: 20px 0 10px;
  }
  input[type="text"], textarea {
    display: block;
    width: 100%;
    padding: 8px;
  }
  #preview {
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
  }
  h3 {
    margin-top: 10px;
  }
  #checkboxes input {
    display: inline-block;
    margin-right: 10px;
  }
  #checkboxes label {
    display: inline-block;
  }
</style>
