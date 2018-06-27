<template>
  <div class="container mx-auto">
    <div class="lg:max-w-lg mx-auto mb-8 pb-10">
      <header class="mb-8">
        <h1 v-html="post.title.rendered" class="text-5xl"></h1>
      </header>
      <main class="text-2xl post-content font-serif" v-html="post.content.rendered"></main>
    </div>
    <no-ssr>
      <related :exclude="parseInt(this.$route.params.id)"/>
    </no-ssr>
  </div>
</template>

<script>

import {FacebookLoader} from 'vue-content-loader';
import Related from '@/components/Related.vue'

export default {
  layout: 'inside',

  components: { Related },

  async asyncData ({ app, params }) {
    const post = await app.$axios.$get(`posts/${params.id}`)
    return { post }
  },

  methods: {
    async getRelatedPosts() {
      const posts = await this.$axios.$get(`posts?per_page=3&exclude=${this.$route.params.id}`)
      return this.related = posts
    }
  },

  head () {
    return {
      title: this.post.title.rendered,
      titleTemplate: '%s | Zeek Interactive'
    }
  }
}
</script>

<style>
  .post-content > p {
    margin-bottom: 1.125em;
    line-height: 1.5;
  }

  .post-content h2,
  .post-content h3, 
  .post-content h4 {
    font-family: 'Source Sans Pro';
    margin-top: 1.125em;
    margin-bottom: .5625em;
  }
</style>
