<template>
    <div id="single-blog">
        <h1>{{ blog.title }}</h1>
        <p>作者: {{ blog.author }}</p>
        <p>分类:</p>
        <ul>
            <li v-for="category in blog.categories" :key=category>
                {{category}}
            </li>
        </ul>
        <article>{{ blog.content }}</article>
    </div>
</template>

<script>
export default {
    name: "single-blog",
    data() {
        return {
            id: this.$route.params.id,
            blog: {},
        };
    },
    created() {
        this.$http
            .get(
                "https://myblog-2be6a-default-rtdb.asia-southeast1.firebasedatabase.app/posts/" +
                    this.id +
                    ".json"
            )
            .then(function (data) {
                console.log(data);
                return data.json();
            })
            .then(function (data) {
                this.blog = data;
            });
    },
};
</script>

<style scoped>
#single-blog {
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
    background: #eee;
    border: 1px dotted #aaa;
}
</style>