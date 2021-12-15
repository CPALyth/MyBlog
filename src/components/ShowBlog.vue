<template>
    <div id="show-blog" v-theme:column="'wide'">
        <h1>博客总览</h1>
        <div v-for="blog in blogs" class="single-blog" :key="blog.title">
            <h2 v-rainbow>{{ blog.title | to-uppercase }}</h2>
            <article>
                {{ blog.body | snippet }}
            </article>
        </div>
    </div>
</template>

<script>
export default {
    name: "show-blog",
    data() {
        return {
            blogs: []
        };
    },
    created() {
        this.$http
            .get("https://jsonplaceholder.typicode.com/posts")
            .then(function (data) {
                this.blogs = data.body.slice(0, 10);
                console.log(this.blogs);
            });
    },
};
</script>

<style>
#show-blog {
    max-width: 800px;
    margin: 0 auto;
}

.single-blog {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>
