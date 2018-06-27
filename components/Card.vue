<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg">
    <img class="w-full" src="https://picsum.photos/400/300/?random"/>
    <div class="px-6 py-4">
      <div class="font-semibold text-xl mb-2">
        <nuxt-link
          :key="post.id" 
          :to="{ name: 'id-slug', params: { slug: post.slug, id: post.id } }" class="no-underline text-black">
          <span v-html="post.title.rendered"></span>
        </nuxt-link>
      </div>
      <div class="text-grey-darker text-base" v-html="post.excerpt.rendered"></div>
    </div>
    <div class="px-6 py-4">
      <span class="inline-block bg-grey-lighter rounded-full px-3 py-1 text-sm font-semibold text-grey-darker mr-2 mb-2">#photography</span>
      <span class="inline-block bg-grey-lighter rounded-full px-3 py-1 text-sm font-semibold text-grey-darker mr-2">#travel</span>
      <span class="inline-block bg-grey-lighter rounded-full px-3 py-1 text-sm font-semibold text-grey-darker">#winter</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>