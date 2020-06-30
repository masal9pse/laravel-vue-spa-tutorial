<template>
  <div class="container">
    <table class="table table-hover">
      <thead class="thead-light">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Title</th>
          <th scope="col">+</th>
          <th scope="col">-</th>
          <th scope="col">Show</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
          <th scope="col">vacation</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task,index) in tasks" :key="index">
          <th scope="row">{{ task.id }}</th>
          <td>{{ task.title }}</td>
          <td>
            <button class="btn btn-dark" @click="task.count++">add</button>
          </td>
          <td>
            <button class="btn btn-warning" @click="task.count--">minus</button>
          </td>
          <td>
            <router-link v-bind:to="{name: 'task.show', params: {taskId: task.id }}">
              <button class="btn btn-primary">Show</button>
            </router-link>
          </td>
          <td>
            <router-link v-bind:to="{name: 'task.edit', params: {taskId: task.id }}">
              <button class="btn btn-success">Edit</button>
            </router-link>
          </td>
          <td>
            <button class="btn btn-danger" @click="deleteTask(task.id)">Delete</button>
          </td>
          <td>{{task.count}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      tasks: []
    };
  },
  methods: {
    getTasks() {
      axios.get("/api/tasks").then(res => {
        this.tasks = res.data;
        console.log(this.tasks);
      });
    },
    deleteTask(id) {
      axios.delete("/api/tasks/" + id).then(res => {
        this.getTasks();
      });
    }
    // addCount(count) {
    //   axios.post("/api/tasks/" + count).then(res => {
    //     res.data.count++;
    //   });
    // },
    // minusCount(todo) {
    //   axios.post("/api/tasks/" + id).then(res => {
    //     res.data.count--;
    //   });
    // }
  },
  mounted() {
    this.getTasks();
  }
};
</script>