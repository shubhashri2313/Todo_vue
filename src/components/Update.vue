<template>
  <div>
    <Header />
<<<<<<< HEAD
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
=======
    <h1>hello user, Welcome to Update Todo List page</h1>
    <form class="update">
      <input type="text" v-model="todo.title" placeholder="Enter title" />
      <input type="text" v-model="todo.description" placeholder="Enter description" />
      <input type="text" v-model="todo.due_date" placeholder="Enter due_date" />
      <input type="text" v-model="todo.completed" placeholder="Enter status" />
      <button type="button" @click="update">Update Todo List</button>
    </form>
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
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
<<<<<<< HEAD
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
=======
      name: '',
      todo: {
        title: '',
        description: '',
        due_date: '',
        completed: ''
      }
    }
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
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
<<<<<<< HEAD
    },
    updateCompleted() {
      if (this.todo.status === 'finished') {
        this.todo.completed = 'yes';
      } else if (new Date(this.todo.due_date) < new Date()) {
        this.todo.completed = 'no';
      } else {
        this.todo.completed = '';
      }
=======
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
    }
  },
  async mounted() {
    console.warn("mounted")
    let user = localStorage.getItem('user info');
<<<<<<< HEAD

    this.name = JSON.parse(user).name;

    if (!user) {
      this.$router.push({ name: 'signUp' });
=======
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({
        name: 'signUp'
      });
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
    }
    console.warn(this.$route.params.id);
    const result = await axios.get(`http://localhost:3000/todo/${this.$route.params.id}`);
    console.warn(result);
    this.todo = result.data; // prefill data
<<<<<<< HEAD

    this.updateCompleted(); // initial update of completed field
=======
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
  }
}
</script>

<style>
</style>
