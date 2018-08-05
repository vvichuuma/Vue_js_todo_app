<template>
  <div class="home">
    <h2>{{ message }}</h2>
    <input type="text" v-model="message">
    <h2>{{ message_2 }}</h2>
    <h2>Length of Task List: {{ numIncompleteTask() }} remaining</h2>
    <button v-on:click="deleteCompleted_tasks()">Clear_Completed_Tasks</button>
    <button v-on:click="addTasks()">Add_tasks</button>
    <h3>Task_id:</h3>  <input type = "text" v-model = "newTasks.id">
    <h3>Task_name:</h3> <input type="text" v-model = "newTasks.text">
    <br>
    <h2>{{ task }}</h2>
    <ul>
       <li v-for="task in tasks">
           {{ task.id }}: <span v-on:click="completeTask(task)" v-bind:class="{strike:task.completion}">{{ task.text }}</span>
       </li>    
    </ul>
  </div>
</template>

<style>
.strike {
  text-decoration: line-through;
}
</style>

<script>
export default {
  data: function() {
    return {
      message: "Vishnu is a pro in programming",
      message_2: "VIshnu is a Computer programmer",
      task: "List of_Tasks",
      tasks: [
        { id: 1, text: "Clean the Dishes", completion: false },
        { id: 2, text: "Iron the Shirts", completion: false },
        { id: 3, text: "Wash the car", completion: false }
      ],

      newTasks: { id: "", text: "", completion: false }
    };
  },
  created: function() {},
  methods: {
    addTasks: function() {
      console.log("Computer Programming", this.newTasks);
      if (this.newTasks.text !== "") {
        this.tasks.push(this.newTasks);
        this.newTasks = { id: "", text: "", completion: false };
      }
    },

    deleteTask: function(inputTask) {
      console.log("task is deleted....", inputTask.text);
      var index = this.tasks.indexOf(inputTask);
      this.tasks.splice(index, 1);
    },

    completeTask: function(inputTask) {
      inputTask.completion = !inputTask.completion;
    },

    numIncompleteTask: function() {
      var count = 0;
      this.tasks.forEach(function(task) {
        if (!task.completion) {
          count += 1;
        }
      });

      return count;
    },

    deleteCompleted_tasks: function() {
      var incompleteTasks = [];
      this.tasks.forEach(function(task) {
        if (!task.completion) {
          incompleteTasks.push(task);
        }
      });

      this.tasks = incompleteTasks;
    }
  },

  computed: {}
};
</script>
