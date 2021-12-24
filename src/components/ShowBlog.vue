<template>
    <div id="show-blog" v-theme:column="'wide'">
        <h1>博客总览</h1>
        <input type="text" v-model="search" placeholder="搜索">
        <div v-for="blog in filteredBlogs" class="single-blog" :key="blog.title">
            <router-link v-bind:to="'/blog/' + blog.id">
                <h2 v-rainbow2>{{ blog.title | toUppercase }}</h2>
            </router-link>
            <article>
                {{ blog.content | snippet }}
            </article>
        </div>
    </div>
</template>

<script>
export default {
    name: "show-blog",
    data() {
        return {
            blogs: [],
            search: ""
        };
    },
    created() {
        this.$http
            .get("https://myblog-2be6a-default-rtdb.asia-southeast1.firebasedatabase.app/posts.json")
            .then(function (data) {
                console.log(data.json());
                return data.json();
            })
            .then(function(data) {
                var blogsArray = [];
                for (let key in data) {
                    console.log(key);
                    console.log(data[key]);
                    data[key].id = key;
                    blogsArray.push(data[key]);
                }
                console.log(blogsArray);
                this.blogs = blogsArray;
            });
    },
    computed: {
        filteredBlogs: function() {
            return this.blogs.filter((blog) => {
                return blog.title.match(this.search)
            })
        }
    },
    filters: {
        toUppercase(value) {
            return value.toUpperCase();
        }
    },
    directives: {
        "rainbow2": {
            bind(el, binding, vnode) {
                el.style.color = "#" + Math.random().toString(16).slice(2,8);
            }
        } 
    }
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

#show-blog a {
    color: #444;
    text-decoration: none;
}

input[type="text"] {
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
}
</style>
