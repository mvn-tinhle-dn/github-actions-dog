<template>
  <div id="app">
    <div class="linked">
      <a href="#/">Home</a> |
      <a href="#/todo">Todo</a> |
      <a href="#/non-existent-path">Broken Link</a>
    </div>
    <component :is="currentView" />
  </div>
</template>

<script >
import Todo from './components/Todo.vue'
import NotFound from './pages/NotFound.vue'
import Home from './pages/Home.vue'


const routes = {
  '/': Home,
  '/todo': Todo,
}

export default {
  name: "App",
  components: { Todo, NotFound, Home },
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
      console.log("sssss")
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