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
            <button class="btn btn-dark">add</button>
          </td>
          <td>
            <button class="btn btn-warning">minus</button>
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
          <td>{{count}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      tasks: [],
      count: 0
    };
  },
  methods: {
    getTasks() {
      axios.get("/api/tasks").then(res => {
        this.tasks = res.data;
      });
    },
    deleteTask(id) {
      axios.delete("/api/tasks/" + id).then(res => {
        this.getTasks();
      });
    }
  },
  mounted() {
    this.getTasks();
  }
};
</script>