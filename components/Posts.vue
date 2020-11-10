<template>
  <div id="blog-home">
      <h1>{{ page_title }}</h1>
      <!-- Create `v-for` and apply a `key` for Vue. Here we are using a combination of the slug and index. -->
      <div v-for="(post,index) in posts"
        :key="post.id + '_' + index">
        <button class="button is-dark">Dark</button>
            <div class="box">
                <!-- <router-link :to="'/blog/' + post.id"> -->
                    <article class="media">
                        <div class="media-left">
                            <figure>
                            <!-- Bind results using a `:` -->
                            <!-- Use a `v-if`/`else` if there is a `featured_image` -->
                            <img
                                v-if="post.featured_image"
                                :src="post.featured_image"
                                alt=""
                            >
                            <img
                                v-else
                                src="http://via.placeholder.com/250x250"
                                alt=""
                            >
                            </figure>
                        </div>
                        
                        <h2>{{ post.titulo }}</h2>
                        <!-- <p>{{ post.summary }}</p> -->
                    </article>
                <!-- </router-link> -->
            </div>
      </div>
  </div>
</template>

<script>
  const axios = require('axios');

  export default {
    name: 'blog-home',
    data() {
      return {
        page_title: 'Blog',
        posts: []
      }
    },
    methods: {
      getPosts() {
        axios.get('http://localhost:1337/posts/')
            .then((response) => {
                this.posts = response.data;
            })
            .catch(function (error) {
                console.log(error);
            })
      }
    },
    created() {
      this.getPosts()
    }
  }
</script>