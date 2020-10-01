<template>
  <div class="container">
    <div class="posts">
      <div class="post-card" v-for="post in $store.state.posts" :key="post.id">
        <div class="post-card-body">
          <p class="title"> 
            <nuxt-link :to="`/blogs/${post.id}`" class="title-link">
              <span @click="updateSelectedPost(post)">
                  {{ post.title }}
              </span>
            </nuxt-link> 
          </p>
          <p class="description">{{ post.body }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  //store to vuex
  fetch({$axios, store}) {
    return $axios.$get("/posts").then(res=> {
      store.commit("updatePosts", res)
    })
  },
  methods: {
    updateSelectedPost(post) {
      this.$store.commit("updateSelectedPost", post);
    }
  }
}
</script>

<style>
.posts {
  display: flex;
  flex-wrap: wrap;
}
.post-card {
  border: 1px solid #333333;
  padding: 15px;
  margin: 10px 15px;
  width: 30%;
  border-radius: 15px;
  text-align: left;
}
.post-card-body .title{
  font-size: 22px;
  font-weight: bold;
  display: block;
}

.post-card-body .title .title-link{
  color: #000000;
}
.post-card-body .description{
  font-size: 18px;
  font-weight: normal;
  display: block;
}
</style>
