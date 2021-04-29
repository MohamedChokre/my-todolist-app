<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Ajouter une tâche
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <HelloWorld @task_added="addTaskList"/>

    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Todo list app</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <div v-for="task in taskList" :key="task" @click="changeColor" id="taskBox"
        v-bind:style="{ backgroundColor: computedBackgroundColor }">
          <h2>{{ task.title }}</h2>
          <p>{{ task.date }}</p>
          <p>{{ task.description }}</p>
          <button @click="modifyTaskIndex(taskList.indexOf(task))" type="button" style="background-color:blue" class="taskAction"></button>
          <button @click="removeTask(taskList.indexOf(task))" type="button" style="background-color:red" class="taskAction"></button>
      </div> 
      <toDo @modify_task="modifyTask" v-show="show"/>
    </v-main> 
  
  </v-app>
</template>

<style>
  #taskBox {
    position : relative;
    margin-left: 15px;
    margin-top: 15px;
    width: 100px;
    height: 200px;
    padding: 10px;
    border-radius: 5px;
    color: white;
  }
  .taskAction {
    position: relative;
    width: 30px;
    height: 30px;
    background-color: white;
  }
</style>

<script>
  import HelloWorld from './components/HelloWorld'
  import toDo from './components/toDo'

  export default {
    data () {
      return {
        drawer: null,
        title: '',
        date: '',
        description: '',
        taskList: [],
        modifyIndex: undefined,
        show: false,
        isDone: false,
        backgroundColor: '#e3e3e3'
      }
    },
    components: {
      HelloWorld,
      toDo
    },
    methods: {
      addTaskList(payload) {
        this.title = payload.title,
        this.date = payload.date,
        this.description = payload.description,
        this.taskList.push({
          title: this.title,
          date: this.date,
          description: this.description,
        })
      },
      removeTask(position) {
        this.taskList.splice(position, 1)
      },
      modifyTaskIndex(number) {
        this.show = true,
        this.modifyIndex = number
      },
      modifyTask(payload) {
        if(this.taskList[this.modifyIndex].title != payload.title && 
          this.taskList[this.modifyIndex].title) {
            this.taskList[this.modifyIndex].title = payload.title
        }
        if(this.taskList[this.modifyIndex].date != payload.date && 
          this.taskList[this.modifyIndex].date) {
            this.taskList[this.modifyIndex].date = payload.date,
            console.log(payload.date)
        }
        if(this.taskList[this.modifyIndex].description != payload.description && 
          this.taskList[this.modifyIndex].description) {
            this.taskList[this.modifyIndex].description = payload.description
        }
        this.show = false
      },
      changeColor() {
        this.isDone = !this.isDone
        if(this.isDone) {
          this.backgroundColor = '#A92000'
        } else {
          this.backgroundColor = '#e3e3e3'
        }
      }
    },
    computed: {
      computedBackgroundColor() {
        return this.backgroundColor
      }
    }
  }
</script>