<template>
  <div class="add-blog">
    <h2>添加博客</h2>
     
    <form v-if="!submitted">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required />
      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <input type="checkbox" value="Vue.js" v-model="blog.categories" />
        <label>Vue.js</label>

        <input type="checkbox" value="Node.js" v-model="blog.categories" />
        <label>Node.js</label>

        <input type="checkbox" value="React.js" v-model="blog.categories" />
        <label>React.js</label>

        <input type="checkbox" value="Angular4" v-model="blog.categories" />
        <label>Angular4</label>
      </div>

      <label>作者:</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author">
          {{ author }}
        </option>
      </select>

      <button @click.prevent="postBlog">添加博客</button>
    </form>

    <div v-if="submitted">
      <h3>您的博客发布成功!</h3>
    </div>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题: {{ blog.title }}</p>
      <p>博客内容:</p>
      <p>{{ blog.content }}</p>
      <p>博客分类:</p>
      <ul>
        <li v-for="category in blog.categories" :key="category">
          {{ category }}
        </li>
      </ul>
      <p>作者: {{ blog.author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-blog",
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
      },
      authors: ["Eward", "Tim", "Bob"],
      submitted: false,
    };
  },
  methods: {
    postBlog: function () {
      this.$http
        .post("https://jsonplaceholder.typicode.com/posts", {
          title: this.blog.title,
          body: this.blog.content,
          userId: 1,
        })
        .then(function (data) {
          // 请求成功
          console.log(data);
          this.submitted = true;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
