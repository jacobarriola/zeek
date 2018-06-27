<template>
  <div class="pb-10">
    <nuxt-link to="/">
      <logo 
      interactiveColor="#000000"
      class="px-4 py-4"/>
    </nuxt-link>
    <nuxt/>
  </div>
</template>

<script>
import Logo from '@/components/Logo.vue';

export default {
  components: {
    Logo
  }
}
</script>

