<script setup>
import { ref } from 'vue';

const listItems = ref([
  // {id:1, label:"10 ice cream"},
  // {id:2, label: "5 oranges"},
  // {id:3, label: "3 sacks of patatoes"}
])

const newItems = ref("")

const isHighPriority = ref(false)

const saveItems = () => {
  listItems.value.push(
    {
      id: listItems.value.length + 1, 
      label: newItems.value
    })
  newItems.value = ""
}

const editing = ref()

const doEdit = (e) => {
  editing.value = e
  newItems.value = ""
}

</script>

<template>
  <div class="header">
    <h1>Shopping List App</h1>
    <button 
      class="btn" 
      v-if="editing" 
      v-on:click="doEdit(false)"
    >
    Cancel</button>
    <button 
      class="btn btn-primary" 
      v-else v-on:click="doEdit(true)"
    >
    Add Items</button>
  </div>
  <form
    @submit.prevent="saveItems"
    v-if="editing"
  >
    <input 
      v-model="newItems"
      type="text"
      placeholder="Add an item"
    >
    <input
      type="checkbox"
      placeholder="high"
      v-model="isHighPriority"
    >High Priority
    <button
      class="btn btn-primary"
      :disabled="newItems.length < 5"
    >
    Save Item</button>
  </form>
  <ul>
    <li
      v-for="{id, label} in listItems"
      :key="id"
    >
    {{ label }}
    </li>
  </ul>
  <p v-if="!listItems.length">Nothing added yet.</p>
</template>

<style>

body {
  background: #eff8ff;
  height: 100vh;
  width: 100vw;
  font-family: system-ui, BlinkMacSystemFont, -apple-system, Segoe UI, Roboto,
    Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 0;
}

.counter {
  font-size: 0.8rem;
  padding-left: 10px;
  padding-right: 10px;
}

#app {
  background: #fff;
  padding: 2rem;
  margin: 1rem;
  border-radius: 3px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.12), 0 2px 4px 0 rgba(0, 0, 0, 0.08);
  width: 95%;
  max-width: 900px;
}

h1 {
  color: #3d4852;
}

ul {
  list-style: none;
  padding: 0;
}

a {
  color: #6cb2eb;
  font-size: 1.25rem;
  transition: all 0.1s ease-in;
  margin-top: 0.5rem;
  display: block;
}

a:hover {
  color: #3490dc;
}

li,
p {
  display: flex;
  align-items: center;
  line-height: 1.75;
  letter-spacing: 0.5px;
  color: #3d4852;
  font-size: 1.25rem;
  cursor: pointer;
  transition: all 0.1s ease-in;
}

li:hover {
  color: #22292f;
}

li input {
  margin: 0 0.5rem 0;
}

#shopping-list > input,
#shopping-list > select {
  width: 100%;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #f1f5f8;
  color: #606f7b;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  font-size: 1rem;
  letter-spacing: 0.5px;
  margin: 0.5rem 0;
}

.add-item-form,
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.add-item-form input {
  width: 70%;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #f1f5f8;
  color: #606f7b;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  font-size: 1rem;
  letter-spacing: 0.5px;
  margin: 0.5rem 0;
}

.btn {
  border: none;
  border-radius: 3px;
  margin: auto 0;
  padding: 0.5rem 0.75rem;
  flex-shrink: 0;
  cursor: pointer;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  transition: all 0.1s ease-in;
}

.btn[disabled] {
  background: #8795a1;
}

.btn[disabled]:hover {
  background: #606f7b;
}

.btn-primary {
  background: #6cb2eb;
  color: #fff;
}

.btn-primary:hover {
  background: #3490dc;
}

.btn-cancel {
  background: #ef5753;
  color: #fff;
}

.btn-cancel:hover {
  background: #e3342f;
  color: #fff;
}

.strikeout {
  text-decoration: line-through;
  color: #b8c2cc;
}

.strikeout:hover {
  color: #8795a1;
}

.priority {
  color: #de751f;
}
input[type="checkbox"]{
  display: inline !important;
  box-shadow: none;
  width: auto;
}

</style>