<template>
  <div
    class="
      relative
      flex
      items-top
      justify-center
      min-h-screen
      bg-gray-100
      sm:items-center sm:pt-0
    "
  >
    <article>
      <h1>{{ post.title }}</h1>
      <p>{{ post.content }}</p>
    </article>
    <div class="mt-8 bg-white overflow-hidden shadow sm:rounded-lg p-6"></div>
    <aside>
      <h3>Posts you might enjoy</h3>
      <ul>
        <li v-for="(related, i) in relatedPosts">
          <nuxt-link :to="`/post/${related.id}`">
            {{ related.title }}</nuxt-link
          >
        </li>
      </ul>
    </aside>
    <nuxt />
  </div>
</template>
<script>
import store from "../../store/index";
export default {
  head() {
    return {
      title: this.post.title,
      meta:  [
        {name: 'twitter:title', content: this.post.title },
        {name: 'twitter:description', content: this.post.content },
        {name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png' }
      ]
    };
  },

  data() {
    return {
      id: this.$route.params.id,
      // post: {},
      posts: this.$store.state.all,
    };
  },

  computed: {
    post() {
      return this.posts.find((post) => post.id === this.id);
    },
    relatedPosts() {
      return this.posts.filter((post) => post.id !== this.id);
    },
  },
};
</script>