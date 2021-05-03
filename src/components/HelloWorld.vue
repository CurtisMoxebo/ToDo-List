<template>
    <v-card elevation="6" width="650px" class="mx-auto px-10 my-5"> 
        <!-- Title -->
        <h2 class="text-center font-weight-bold headline py-2">Todo List</h2>

        <!-- Section for the addition of a new task -->
          <h3 class="font-weight-medium">Add Task</h3>
          <v-divider color="black" class="mb-6" ></v-divider>

          <v-layout row>
              <v-flex xs11>
                  <v-text-field solo label="Write a new task and press enter" class="ml-3 mr-4" height="50px" > </v-text-field>
              </v-flex>

              <v-flex xs1>
                  <v-btn text height="50px" max-width="20px" class="blue--text" >+ Add</v-btn>
              </v-flex>
          </v-layout>
        <!-- End section -->
        
        <!-- Section for todo task -->
          <h3 class="font-weight-medium mt-5">To Do</h3>
          <v-divider color="black" class="mb-2" ></v-divider>
        <!-- End section -->

        <!-- Section for completed task -->
          <h3 class="font-weight-medium mt-1">Completed</h3>
          <v-divider color="black" class="mb-2" ></v-divider>
        <!-- End section -->

    </v-card>
</template>

<script>
  export default {
    name: 'HelloWorld',
  }
</script>
