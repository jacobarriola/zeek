<template>
  <div>
    <div class="text-3xl mb-8 font-bold">More Articles from Zeek</div>
    <div class="flex items-stretch -mx-4">
      <span v-if="loading">
        <facebook-loader class="w-1/3 px-4"></facebook-loader>
        <facebook-loader class="w-1/3 px-4"></facebook-loader>
        <facebook-loader class="w-1/3 px-4"></facebook-loader>
      </span>
      <div v-else class="w-1/3 px-4 flex" v-for="post in related" :key="post.id">
        <Card :post="post"/>
      </div>
    </div>
  </div>
</template>

<script>
import { FacebookLoader } from 'vue-content-loader'
import Card from '@/components/Card.vue'

export default {
  props: {
    exclude: {
      type: Number
    }
  },
  
  components: { FacebookLoader, Card },

  data() {
    return {
      related: [],
      loading: true,
      error: false
    }
  },

  methods: {
    async getRelatedPosts() {
      try {
        const posts = await this.$axios.$get(`posts?per_page=3&exclude=${this.exclude}`)
        this.related = posts
        this.loading = false
        return
      } catch (error) {
        return this.error = true
      }
    }
  },

  mounted() {
    window.setTimeout(() => {
      this.getRelatedPosts()
    }, 10000)
  }
}
</script>
