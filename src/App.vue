<template>
  <main>
    <header>
      <h1>ToDo</h1>
      <span @click="showAddTask = !showAddTask" class="newbtn">
        <span v-if="showAddTask">X</span>
        <span v-else class="newbtn-plus">+</span>
      </span>
    </header>
    <div v-if="showAddTask" class="addTask">
      <input v-model="taskText" type="text" placeholder="Type new task..">
      <button @click="addTask" class="taskbtn">Add Task</button>
    </div>
    <div class="todos">
      <div v-for="task in tasks" :key="task.id" class="todo">
        <p class="text">{{task.text}}</p>
        <p class="date">{{task.date}}</p>
        <span @click="removeTask(task.id)" class="remove">X</span>
      </div>
      <!-- <div class="todo">
        <p class="text">Lorem ipsum dolor sit amet Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quaerat tempore id amet! Quaerat perferendis odio laborum, numquam vitae, sint beatae ad dolorem consectetur doloremque ipsam vero fugiat soluta animi ullam.</p>
        <p class="date">12/12/22</p>
        <span class="close">X</span>
      </div> -->
    </div>
  </main>
</template>

<script setup>
  import {ref} from 'vue'

  const showAddTask = ref(false)
  const taskText = ref("")
  const tasks = ref([
    // {
    //   id: Math.floor(Math.random()*100000),
    //   text: "lorem ipsum",
    //   date: new Date().toLocaleDateString()
    // }
  ])
  function addTask(){
    if(!taskText.value) return
    tasks.value.push({
      id: Math.floor(Math.random()*100000),
      text: taskText.value,
      date: new Date().toLocaleDateString()
    })
    taskText.value = ""
  }
  function removeTask(id){
    tasks.value = tasks.value.filter(i => {return i.id !== id})
  }
</script>

<style scoped>
  main{
    background-color: aliceblue;
    min-height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    gap: 1rem;
  }
  header{
    display: flex;
    align-items: center;
    height: fit-content;
    width: 80%;
    justify-content: space-between;
    position: sticky;
    top: 0px;
    z-index: 10;
    margin-bottom: 10px;
    background-color: aliceblue;
  }
  h1{
    font-family: cursive;
    font-size: 2.5rem;
    font-weight: bold;
  }
  .newbtn{
    height: 30px;
    width: 30px;
    border: 0;
    border-radius: 50%;
    color: aliceblue;
    background-color: darkblue;
    font-weight: bold;
    font-size: 1.2rem;
    display: grid;
    place-items: center;
    cursor: pointer;
    user-select: none;
    /* line-height: 0; */
    /* text-align: center; */
  }
  .newbtn-plus{
    font-size: 1.3rem;
    font-weight: bold;
    line-height: 0;
  }
  .todos{
    width: 80%;
    gap: 1rem;
  }
  .todo{
    background-color: cornsilk;
    display: flex;
    justify-content: space-between;
    padding: 1rem;
    margin-bottom: 1rem;
    border-radius: 10px;
    box-shadow: 5px 5px 5px rgba(0,0,0,0.1);
  }
  .todo .text{
    width: 70%;
  }
  .todo span{
    cursor: pointer;
    user-select: none;
    font-family: monospace;
    color: orangered;
  }
  .addTask{
    width: 80%;
    background-color: azure;
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
    display: flex;
    justify-content: space-around;
    margin-bottom: 10px;
  }
  input{
    width: 70%;
    border-radius: 10px;
    border: 1px solid aqua;
    padding: 10px;
    outline: none;
  }
  .taskbtn{
    padding: 10px;
    color: aliceblue;
    border: 0;
    outline: none;
    border-radius: 10px;
    background-color: darkslateblue;
  }
  .remove{
    margin-left: 10px;
  }

  @media (max-width: 500px) {
    header{
      width: 100vw;
      padding: 0 15px 0 15px;
      box-shadow: 0px 5px 5px rgba(0,0,0,0.1);
    }
    .addTask{
      width: 95%;
    }
    .todos{
      width: 95%;
    }
  }
</style>