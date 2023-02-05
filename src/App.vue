<template>
  <div class="container">
    <Header  title="Task Traker"/>
    <AddTask @add-task="addTask" />
    <Tasks 
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask" :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {

    addTask(task){
      this.tasks = [...this.tasks, task];
    },

    deleteTask(id){
      this.tasks = this.tasks.filter((task) => task.id !==id)
    },
  //  This is from chatGPT
    // deleteTask(id) {
    // const index = this.tasks.findIndex(task => task.id === id);
    // if (index !== -1) {
    //   this.tasks.splice(index, 1);
    // }
  //}
  // toggleReminder(id) {
  //   this.tasks = this.tasks.map((task)=>task.id === id ? {...task, reminder: !task.reminder}: task) 
  // }

  toggleReminder(id) {
  const index = this.tasks.findIndex(task => task.id === id);
  if (index !== -1) {
    const task = this.tasks[index];
    this.tasks.splice(index, 1, { ...task, reminder: !task.reminder });
  }
}

  },
  created(){
    this.tasks = [
      {
        id:1,
        text: 'Replace windows 7 desktop',
        day: "Feb 7 at 2:30pm",
        reminder: false
      },

      {
        id:2,
        text: 'Printer connection issue',
        day: "Feb 8 at 2:30pm",
        reminder: true
      },

      {
        id:3,
        text: 'Fix internet connection issue',
        day: "Feb 9 at 2:30pm",
        reminder: false
      },

      {
        id:4,
        text: 'Deploy new chrombox',
        day: "Feb 10 at 2:30pm",
        reminder: true
      },
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
