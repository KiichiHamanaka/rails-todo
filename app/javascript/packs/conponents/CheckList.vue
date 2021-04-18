<template>
  <div>
    <div>
      <input v-model="newTask">
      <button @click="createTask">追加</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks">
        <input type="checkbox" v-model="task.is_done" @click="update(task.id, checkList)">
        <span :class="{done: task.is_done}">{{ task.name }}</span>
        <button @click="deleteTask(task.id, checkList)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
const url =`http://localhost:5000/api/tasks/`

export default {
  data() {
    return {
      tasks: [],
      newTask: ''
    }
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    // APIからタスク一覧を取得
    fetchTasks: function () {
      axios.get(url).then((response) => {
        for(let i = 0; i < response.data.tasks.length; i++) {
          this.tasks.push(response.data.tasks[i]);
        }
      }, (error) => {
        console.log(error, response);
      });
    },
    createTask() {
      if(this.newTask == '') return;
      axios.post(url, { task: { name: this.newTask } }).then((response) => {
        this.tasks.unshift(response.data);
        this.newTask = '';
      }, (error) => {
        console.log(error, response);
      });
    },
    deleteTask: function (task_id, index) {
      axios.delete(url + task_id).then((response) => {
        this.tasks.splice(index, 1);
      }, (error) => {
        console.log(error, response);
      });
    },
    update(task_id) {
      axios.put(url + task_id).then((response) => {
      }, (error) => {
        console.log(error);
      });
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>