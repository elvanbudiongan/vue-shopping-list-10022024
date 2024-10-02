<template>
  <div id="app">
    <header>
      <h1>My Shopping List App</h1>
    </header>

    <!-- Include ShoppingList component -->
    <ShoppingList />

  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ShoppingList from './components/ShoppingList.vue'; // Import the ShoppingList component

export default defineComponent({
  name: 'App',
  components: {
    ShoppingList, // Register the ShoppingList component
  },
});
</script>

<style scoped>
#app {
  text-align: center;
  margin-top: 20px;
  background: none;
  padding: 10px;
  border-radius: 10px;
  border: 2px solid #2baaff;
}

header {
  background-color: #f8f9fa;
  padding: 20px;
  color: Black;
}
header h1{
  size: 40px;
}
</style>
