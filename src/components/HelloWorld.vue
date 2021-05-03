<template>
    <v-card elevation="6" width="650px" class="mx-auto px-10 my-5"> 
        <!-- Title -->
        <h2 class="text-center font-weight-bold headline py-2">Todo List</h2>

        <!-- Section for the addition of a new task -->
          <h3 class="font-weight-medium">Add Task</h3>
          <v-divider color="black" class="mb-6" ></v-divider>

          <v-layout row>
              <v-flex xs11>
                <v-text-field solo id="newTask" ref="newTask" label="Write a new task and press enter" class="ml-3 mr-4" height="50px"  v-on:keyup.enter="addTask"> </v-text-field>
              </v-flex>

              <v-flex xs1>
                  <v-btn text height="50px" max-width="20px" class="blue--text" @click="addTask">+ Add</v-btn>
              </v-flex>
          </v-layout>
        <!-- End section -->
        
        <!-- Section for todo task -->
          <h3 class="font-weight-medium mt-5">To Do</h3>
          <v-divider color="black" class="mb-2" ></v-divider>

          <v-container>
          <!-- iterate and display the uncompleted tasks in todo list -->
          <div v-for="(item, index) in todoList" :key="`task-${index}`" >
              <v-layout row v-if="!item.isCompleted">
                  <v-flex xs1>
                      <v-checkbox align="end" justify="end" :input-value="item.isCompleted" @click="completeTask(index)"></v-checkbox>
                  </v-flex>

                  <v-flex xs10>
                      <v-text-field :flat="!item.isEditable" :disabled="!item.isEditable" v-on:keyup.enter="changeIsEditable(index)" solo :id="'task'+index" label="New task" min-height="20px" class= "black--text" :value="item.task"> </v-text-field>
                  </v-flex>

                  <v-flex xs1 class="pl-4">
                      <v-btn text height="25px" max-width="20px" class="green--text" @click="changeIsEditable(index)" >Edit</v-btn>
                      <v-btn text height="25px" max-width="20px" class="red--text mt-2" @click="deleteTask(index)" >delete</v-btn>
                  </v-flex>
              </v-layout>

              <v-divider class="mb-4" v-if="!item.isCompleted"></v-divider>
            </div>
          </v-container>
        <!-- End section -->

        <!-- Section for completed task -->
          <h3 class="font-weight-medium mt-1">Completed</h3>
          <v-divider color="black" class="mb-2" ></v-divider>

          <v-container>
            <!-- iterate and display the completed tasks in todo list -->
            <div v-for="(item, index) in todoList" :key="`task-${index}`">
              <v-layout row v-if="item.isCompleted">
                  <v-flex xs1>
                      <v-checkbox :input-value="item.isCompleted" @click="reassignTask(index)"></v-checkbox>
                  </v-flex>

                  <v-flex xs10>
                      <v-text-field :flat="!item.isEditable" :disabled="!item.isEditable" v-on:keyup.enter="changeIsEditable(index)" solo :id="'task'+index" label="New task" min-height="50px" class= "text-decoration-line-through" :value="item.task"> </v-text-field>
                  </v-flex>

                  <v-flex xs1 class="pl-4">
                      <v-btn text height="25px" width="20px" class="green--text mr-14" @click="changeIsEditable(index)">Edit</v-btn>
                      <v-btn text height="25px" width="20px" class="red--text mt-2 mr-14" @click="deleteTask(index)">delete</v-btn>
                  </v-flex>
              </v-layout>

              <v-divider class="mb-4" v-if="item.isCompleted"></v-divider>
            </div>
            <!-- End section -->

        </v-container>
    </v-card>
</template>

<script>
  export default {
    name: 'HelloWorld',

    //receive todo list from App.vue as a prop
    props: ['todoList'],

    methods: {
      
      //Get and send new task to todoList
      addTask(){
          let newTask = document.getElementById('newTask');

          //check if input is not empty first
          if(newTask.value){
              this.$emit('addTask', newTask.value);
              this.$refs.newTask.reset();
          }
      },

      //Get and send a completed task to todoList
      completeTask(index){
          this.$emit('completeTask', index);
      },

      //Get and send task to be reassigned a task to todoList
      reassignTask(index) {
          this.$emit('reassignTask', index);
      }, 

      //Get and send edited task to todoList
      changeIsEditable(index){
          let editedTask = document.getElementById("task"+index);
          this.$emit('changeIsEditable', index, editedTask.value);
      },

      //Get and send task to be deleted to todoList
      deleteTask(index){
          this.$emit('deleteTask', index);
      },
    }
  }
</script>
