<template>
  <v-app dark>
    <h1 v-if="error.statusCode === 404">
      {{ pageNotFound }}
    </h1>
    <h1 v-else>
      {{ otherError }}
    </h1>
    <NuxtLink to="/">
      Home page
    </NuxtLink>
  </v-app>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from '@vue/composition-api'

export default defineComponent({
    layout: 'empty',
    props: {
      error: {
        type: Object,
        require: false,
        default: () => ({ statusCode: 0 })
      }
    },
    setup({ error }){
      const state = reactive({
        pageNotFound: '404 Not Found',
        otherError: 'An error occurred'
      })

      const head = error.statusCode === 404 ? state.pageNotFound : state.otherError

      return { ...toRefs(state), head }
    }
})
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
