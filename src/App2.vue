<!--Optional-->
<script>
export default {
  data() {
    return {
      name: 'Vuelearning',
      status: 'Pending',
      tasks: ['Task 1', 'Task 2', 'Task 3', 'Task 4', 'Task 5'],
      link: 'https://vuejs.org/guide/essentials/class-and-style.html',
    };
  },
  methods: {
    toggleStatus(){
      if(this.status === 'active'){
        this.status = 'Pending';
      } else if(this.status === 'Pending'){
        this. status = 'Inactive';
      } else {
        this.status = 'active';
      }
    },
  },
}
</script>
<template>
  <h1>{{name}}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'Pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{task}}</li>
  </ul>
<!--  <a v-bind:href="link">Click for Vue</a>-->
  <a :href="link">Click for VueJs</a>
  <br />
<!--  <button v-on:click="toggleStatus">Change Status</button>-->
  <button @click="toggleStatus">Change Status</button>

</template>

<!--conditional-->
<script setup>
import {onMounted, ref} from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['task1', 'task2', 'task3']);
const newTask = ref('')

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'Pending';
  } else if (status.value === 'Pending') {
    status.value = 'Inactive';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== ''){
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log('Error while fetching data');
  }
});

</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'Pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <br/>
  <!--  <button v-on:click="toggleStatus">Change Status</button>-->
  <button @click="toggleStatus">Change Status</button>

</template>

