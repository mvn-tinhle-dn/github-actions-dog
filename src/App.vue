<template>
  <div id="app">
    <div class="linked">
      <a href="#/">Todo</a> |
      <a href="#/non-existent-path">Broken Link</a>
    </div>
    <component :is="currentView" />
  </div>
</template>

<script >
import Todo from './components/Todo.vue'
import NotFound from './pages/NotFound.vue'


const routes = {
  '/': Todo,
}

export default {
  name: "App",
  components: { Todo, NotFound },
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  }
}
</script>

<style scoped>
#app {
  width: 100vw;
  height: 100vh;
  display: block;
}

.linked {
  margin-bottom: 20px;
}
</style>