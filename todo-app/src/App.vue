<template>
  <div id="app">
    <img src="./assets/logo.png">
    <Navigation>
    </Navigation>
    <router-view/>
    <!-- We use kebab-case in our HTML per vue style guides -->
    <todo-list>
    </todo-list>
  </div>
</template>

<script>

// import our own modules here
import TodoList from './components/TodoList'
import Navigation from './components/Navigation'
export default {
  name: 'App',
  components: {
    // We use camelCase within JavaScript per vue style guides
    // read more here: https://vuejs.org/v2/style-guide/#Prop-name-casing-strongly-recommended
    TodoList,
    Navigation
  }
  // data function is put in our main App.vue, NOT the component itself
  // TODO: adapt data used in TailWindUI to match format given here: https://scotch.io/tutorials/build-a-to-do-app-with-vue-js-2
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
