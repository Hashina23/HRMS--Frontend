<template>
  <v-app>
    <sidebar/>
    <v-main style="background-color: #B3BFB8;">
      <v-container>
        <nuxt class="mt-5"/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import sidebar from '@/components/layouts/sidebar.vue';
export default {
  name: 'DefaultLayout',
  components: {
    sidebar
  }
}
</script>
