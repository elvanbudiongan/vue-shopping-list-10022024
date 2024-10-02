<template>
  <div class="shopping-list">
    <h2>Shopping List</h2>

    <!-- Form to add new items -->
    <form @submit.prevent="addItem">
      <input v-model="newItem" placeholder="Enter new item" />
      <button type="submit">Add</button>
    </form>

    <!-- List of shopping items -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <input
          type="checkbox"
          v-model="item.checked"
        />
        <span :class="{ 'checked': item.checked }">{{ item.label }}</span>

        <!-- Edit button -->
        <button @click="editItem(index)">Edit</button>

        <!-- Delete button -->
        <button @click="deleteItem(index)">Delete</button>
      </li>
    </ul>

    <!-- Form to edit an item  not yet implemented-->

  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

interface ShoppingItem {
  label: string;
  checked: boolean;
}

export default defineComponent({
  name: 'ShoppingList',
  setup() {
    // Reactive state
    const items = ref<ShoppingItem[]>([]); // List of items
    const newItem = ref<string>('');       // For adding new item
    const editingIndex = ref<number | null>(null); // Track the item being edited
    const editingValue = ref<string>('');  // Temporary value for the edit form
    const isEditing = ref<boolean>(false); // Toggle for editing mode

    // Add a new item to the list
    const addItem = () => {
      if (newItem.value.trim()) {
        items.value.push({
          label: newItem.value,
          checked: false,
        });
        newItem.value = ''; // Clear the input
      }
    };

    // Delete an item from the list
    const deleteItem = (index: number) => {
      items.value.splice(index, 1);
    };

    // Prepare to edit an item
    const editItem = (index: number) => {
      editingIndex.value = index;
      editingValue.value = items.value[index].label;
      isEditing.value = true; // Enable the edit form
    };

    // Update the item after editing
    const updateItem = () => {
      if (editingIndex.value !== null && editingValue.value.trim()) {
        items.value[editingIndex.value].label = editingValue.value;
        isEditing.value = false; // Close the edit form
        editingIndex.value = null; // Clear the edit state
        editingValue.value = ''; // Clear the input
      }
    };

    return {
      items,
      newItem,
      addItem,
      deleteItem,
      editItem,
      updateItem,
      editingValue,
      isEditing,
    };
  },
});
</script>

<style scoped>
.checked {
  text-decoration: line-through;
}

ul {
  list-style-type: none;
  padding: 0;
}

button {
  margin-left: 10px;
  padding: 5px;
  width: 50px;
  border-radius: 10px;
  background: yellowgreen;
}

button:hover {
  background: pink;
}

form {
  margin-bottom: 20px;
}
</style>
