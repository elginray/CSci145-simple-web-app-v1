<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->

<template>
    <div class="simple-todo">
      <div class="title has-text-centered">
        Simple To Do List in Vue
      </div>

      <form
      @submit.prevent="addTodo"
      >
        <div class="field is-grouped mb-5">
      <p class="control is-expanded">
        <input 
        v-model="newTodoContent"
        class="input" 
        type="text" 
        placeholder="Add a Task">
      </p>
      <p class="control">
        <button 
        :disabled="!newTodoContent"
        class="button is-info"
        >
          Add
        </button>
      </p>
    </div>
      </form>

      <div 
      v-for="todo in todos"
      class="card mb-5"
      >
      <div class="card-content">
        <div class="content">

          <div class="columns is-mobile is-vcentered">
            <div class="column is-5 has-text-right">
              {{ todo.content }}
            </div>
            <div class="column">
              <button class="button is-light">
              &check;
              </button>
              <button
                @click="deleteTodo(todo.id)"
                class="button is-danger ml-2">
              &cross;
              </button>
            </div>
          </div>


        </div>
      </div>
    </div>



</div>
</template>


<script setup>
  /* 
  imports
  */

  import { Comment, ref }  from 'vue'
  import { v4 as uuidv4 } from 'uuid';

  /*
  todos
  */

  const todos = ref([
    {
    id: 'id1',
    content: 'Finish the simple-web-app for CSci 145 Platforms Development',
    done: false
    },
    {
    id: 'id2',
    content: 'Deploy app to netlify',
    done: false,
    }
  ])
  
  /* 
    add todo
  */
  
  const newTodoContent = ref('')
  const addTodo = () => {
    console.log('add todo') 
    const newTodo = {
      id: uuidv4(),
      content: newTodoContent.value,
      done: false
    }
  
  todos.value.unshift(newTodo)
  newTodoContent.value = ''
}

/*
delete todo
*/

const deleteTodo = id => {
  todos.value = todos.value.filter(todo => todo.id !== id)
  console.log('deleteTodo:', id)
}

</script>



<style>
@import 'bulma/css/bulma.min.css';

.simple-todo{
  max-width: 400;
  padding: 20px;
  margin: 0 auto;
}   
</style>