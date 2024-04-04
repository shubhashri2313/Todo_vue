<template>
  <div>
    <Header />
    <div class="container mt-5">
      <h1><i class="fas fa-edit"></i> Update Todo List</h1>
      <form class="update mt-4">
        <div class="mb-3">
          <label for="title" class="form-label">Title</label>
          <input type="text" id="title" v-model="todo.title" class="form-control" placeholder="Enter title" />
        </div>
        <div class="mb-3">
          <label for="description" class="form-label">Description</label>
          <input type="text" id="description" v-model="todo.description" class="form-control" placeholder="Enter description" />
        </div>
        <div class="mb-3">
          <label for="due_date" class="form-label">Due Date</label>
          <input type="date" id="due_date" v-model="todo.due_date" class="form-control" placeholder="Enter due_date" />
        </div>
        <div class="mb-3">
          <label for="status" class="form-label">Status</label>
          <select id="status" v-model="todo.status" class="form-select">
            <option value="todo">Todo</option>
            <option value="in progress">In Progress</option>
            <option value="finished">Finished</option>
          </select>
        </div>
        <button type="button" @click="update" class="btn btn-primary"><i class="fas fa-save"></i> Update Todo List</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'

export default {
  name: 'Update',
  components: {
    Header
  },
  data() {
    return {
      todo: {
        title: '',
        description: '',
        status: '',
        due_date: '',
        completed: ''
      }
    };
  },
  watch: {
    'todo.status': 'updateCompleted',
    'todo.due_date': 'updateCompleted',
  },
  methods: {
    async update() {
      try {
        let result = await axios.put(`http://localhost:3000/todo/${this.$route.params.id}`, this.todo);
        if (result.status == 200) {
          this.$router.push({ name: 'Home' });
        }
        console.warn("result", result);
      } catch (error) {
        console.error("Error updating todo:", error);
      }
    },
    updateCompleted() {
      if (this.todo.status === 'finished') {
        this.todo.completed = 'yes';
      } else if (new Date(this.todo.due_date) < new Date()) {
        this.todo.completed = 'no';
      } else {
        this.todo.completed = '';
      }
    }
  },
  async mounted() {
    console.warn("mounted")
    let user = localStorage.getItem('user info');

    this.name = JSON.parse(user).name;

    if (!user) {
      this.$router.push({ name: 'signUp' });
    }
    console.warn(this.$route.params.id);
    const result = await axios.get(`http://localhost:3000/todo/${this.$route.params.id}`);
    console.warn(result);
    this.todo = result.data; // prefill data

    this.updateCompleted(); // initial update of completed field
  }
}
</script>

<style>
</style>
