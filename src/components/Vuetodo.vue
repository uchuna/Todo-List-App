<template>
    <!-- Wraps the entire content inside a div with the class name 'container'. -->
    <div class="container">
        <!-- Displays the header 'Vue TO DO App'. -->
        <h1>Vue TO DO App</h1>
        <!-- Creates an input field that uses 'v-model' to bind the input value to the newTask data property. The @keyup.enter="addTask" listens for the Enter key press and triggers the addTask method. -->
        <input v-model="newTask" @keyup.enter="addTask" placeholder="Add New Task">
        <!-- <ul> and <li>: Creates an unordered list where each list item (<li>) represents a task. -->
        <ul>
            <li v-for="(task, index) in tasks" :key="index"> <!-- Loops through the tasks array, displaying each task and binding its index as a unique key. -->
                <span v-if="index !== editedTaskIndex"> {{ task }} </span> <!-- Displays the task content as a text if the current index is not the one being edited. -->

                <!-- Displays an input field (to edit the task) when the index matches editedTaskIndex. Binds its value to updatedTask and listens for Enter key press or blur event (losing focus) to update or cancel the update. -->
                <input v-else v-model="editedTask" @keyup.enter="updateTask" @blur="cancelUpdate">
                <div>
                    <!-- Buttons to update and delete tasks, respectively. They call the updateTask and deleteTask methods, passing the index of thupe task. -->
                    <button @click="editTask(index)">Update</button>
                    <button @click="deleteTask(index)">Delete</button>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    
    data() { // Contains the component's data properties.
        return {
            newTask: "", // Holds the value of the input field for adding a new task.
            tasks: [], // Array to store all tasks.
            editedTask: "", // Holds the content of the task being updated
            editedTaskIndex: -1 // Stores the index of the task being edited (-1 indicates no task is being edited).
        };
    },
    methods: { // Contains the methods used in the template section to manipulate tasks (add, update, cancel update, delete).
        addTask() {
            if (this.newTask.trim() !== "") {
                this.tasks.push(this.newTask);
                this.newTask = "";
            }
        },
        editedTask(index) {
            this.editedTaskIndex = index;
            this.editedTask = this.tasks[index];
        },
        editTask() {
            if (this.editedTask.trim() !== "") {
                this.tasks[this.editedTaskIndex] = this.editedTask;
                this.editedTask = "";
                this.editedTaskIndex = -1
            }
        },
        cancelUpdate() {
            this.editedTask = "";
            this.editedTaskIndex = -1;
        },
        deleteTask(index) {
            this.tasks.splice(index, 1);
        }
    }
};
</script>

<style lang="scss" scoped>
.container {
    font-family: Arial, sans-serif;
    max-width: 400px;
    margin: 20px auto;
    padding: 20px;
    background-color: #ee9a9a;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(228, 169, 169, 0.1);

    h1 {
        text-align: center;
        margin-bottom: 20px;
    }

    input {
        width: calc(100%);
        padding: 10px;
        margin-bottom: 10px;
        border: 1px solid #ccc;
        border-radius: 3px;
        box-sizing: border-box;
    }

    ul {
        list-style: none;
        padding: 0;

    li {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 8px;
        background-color: #fff;
        border-radius: 5px;

      button {
        background-color: #ff6347;
        color: #fff;
        border: none;
        padding: 5px 10px;
        border-radius: 3px;
        cursor: pointer;
        margin: 2px;
      }
    }
  }
}
</style>