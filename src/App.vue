<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
     <label>New todo</label>
     <input v-model="newTodo" name="newTodo">
     <button>Add New Todo</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <h3>{{todo.content}}</h3>
    </li>
  </ul>
  
  <!-- <h2>{{newTodo}}</h2> -->
</template>

<script>
import { ref } from 'vue';
// import { ref, reactive } from 'vue';
export default {
// data:
// methods:
// computed:
setup()  {
  // const data = reactive({
  //   newTodo: '',
  //   todos: [],
  // })
  const newTodo = ref('');
  const todos = ref([]);
  function addNewTodo(){
    todos.value.push({
      id: Date.now(),
      done: false,
      content: newTodo.value,
    });
    // console.log(newTodo.value);
    // console.log('form was submitted');
  }
  return{
    todos,
    newTodo,
  addNewTodo,
  };
}
}
</script>



<style scoped>
button{
  background-color: blue;
  color:white
}
h1{
color: black;
text-align: center;
}
form{
  display: block;
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  width: 80%;
  margin: auto;
  text-align: center;
}
input, textarea, button, p , div, section, article, select {
  display: block;
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
 
 }
</style>
