<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
        <HelloWorld :todoList= "todoList" @addTask="addTask" @completeTask="completeTask" @reassignTask="reassignTask" @changeIsEditable="changeIsEditable" @deleteTask="deleteTask" />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
      //Create todo list
      todoList : [
          {task: 'Go to work', isCompleted: false, isEditable: false},
          {task: 'Do your grocery', isCompleted: false, isEditable: false},
          {task: 'Time for launch', isCompleted: true, isEditable: false}
      ],
  }),

  methods: {
      //Addition of new task to todo list
      addTask(text){
          this.todoList.push({task: text, isCompleted: false, isEditable: false});
      },

      //Set task to complete
      completeTask(index){
          this.todoList[index].isCompleted = true;
      },

      //Set task to uncomplete
      reassignTask(index){
          this.todoList[index].isCompleted = false;
      },

      //Edit and save task to todo list
      changeIsEditable(index, text){
          console.log('im in here');
          if(this.todoList[index].isEditable){
              this.todoList[index].task = text;
              this.todoList[index].isEditable = false;
          }

          else{
              this.todoList[index].isEditable = true;
          }
      },

      //Delete task from todo list
      deleteTask(index){
          this.todoList.splice(index, 1);
      }
  }
};
</script>
