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

    <v-main id="main">
      <section>
        <div v-for="task in taskList" :key="task" id="taskBox">
            <h2>{{ task.title }}</h2>
            <p>{{ task.date }}</p>
            <p>{{ task.description }}</p>
            <button @click="modifyTaskIndex(taskList.indexOf(task))" type="button" style="background-color:blue" class="taskAction"></button>
            <button @click="removeTask(taskList.indexOf(task))" type="button" style="background-color:red" class="taskAction"></button>
            <button @click="task.isDone = !task.isDone" type="button" style="background-color:green; width:75px" class="taskAction">
              <p v-if="task.isDone == true">Fait</p>
              <p v-else>Non fait</p>
            </button>
        </div> 
        <toDo @modify_task="modifyTask" @cancel_modification="cancelModificationAction" v-show="show"/>
      </section>
    </v-main>
  
  </v-app>
</template>

<style>
  section {
    position: relative;
    display: Flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: flex-start;
    width: 100%;
    height: auto;
    padding-bottom: 12px;
  }
  #taskBox {
    position : relative;
    margin-left: 15px;
    margin-top: 15px;
    width: 100px;
    height: 200px;
    padding: 10px;
    border-radius: 5px;
    background-color: #e3e3e3;
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
          isDone: false
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
        if(this.taskList[this.modifyIndex].title != payload.title) {
            this.taskList[this.modifyIndex].title = payload.title
        }
        if(this.taskList[this.modifyIndex].date != payload.date) {
            this.taskList[this.modifyIndex].date = payload.date,
            console.log(payload.date)
        }
        if(this.taskList[this.modifyIndex].description != payload.description) {
            this.taskList[this.modifyIndex].description = payload.description
        }
        this.show = false
      },
      cancelModificationAction(payload) {
        this.show = payload.show
      }
    }
  }
</script>