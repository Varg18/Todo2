<template>
  <v-app class="App">
    <v-main>
      <todoPage/>
    </v-main>
  </v-app>
</template>

<script>
import todoPage from "@/components/todo-page";
export default {
  name: 'App',
  components: {todoPage},
  data: () => ({

  }),
}
</script>
<style scoped lang="sass">
.App
  text-align: center
  height: 100vh
  background-color: #312E81
</style>
