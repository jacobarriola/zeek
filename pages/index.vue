<template>
  <div>
    <hero/>
    
    <div class="container mx-auto">

      <div class="py-10">
        <div class="flex justify-between border-b-2 border-red mb-8 pb-2">
          <span class="uppercase font-semibold">Blog Posts</span>
        </div>
        <div class="flex items-stretch -mx-4">
          <div
            class="w-1/3 px-4 flex"
            v-for="post in blogPosts"
            :key="`post-${post.id}`">
            <card :post="post" />
          </div>
        </div>
      </div>

      <div class="py-10">
        <div class="flex justify-between border-b-2 border-red mb-8 pb-2">
          <span class="uppercase font-semibold">WordPress</span>
        </div>
        <div class="flex items-stretch -mx-4">
          <div
            class="w-1/3 px-4 flex"
            v-for="post in wpPosts"
            :key="`wp-${post.id}`">
            <card :post="post" />
          </div>
        </div>
      </div>

      <div class="py-10">
        <div class="flex justify-between border-b-2 border-red mb-8 pb-2">
          <span class="uppercase font-semibold">How To</span>
        </div>
        <div class="flex items-stretch -mx-4">
          <div
            class="w-1/3 px-4 flex"
            v-for="post in howToPosts"
            :key="`ht-${post.id}`">
            <card :post="post" />
          </div>
        </div>
      </div>

    </div>

  </div>
</template>

<script>
import Logo from "~/components/Logo.vue"
import Card from "~/components/Card.vue"
import Hero from "~/components/Hero.vue"

export default {
  components: {
    Logo,
    Card,
    Hero
  },
  async asyncData({ app }) {
    const blogPosts = await app.$axios.$get("posts?categories=41&per_page=3");
    const howToPosts = await app.$axios.$get("posts?categories=99&per_page=3");
    const wpPosts = await app.$axios.$get("posts?categories=16&per_page=3");
    return { blogPosts, howToPosts, wpPosts };
  }
};
</script>
