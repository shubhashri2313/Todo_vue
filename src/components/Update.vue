<template>
  <div>
    <Header />
    <h1>hello user, Welcome to Update Todo List page</h1>
    <form class="update">
      <input type="text" v-model="todo.title" placeholder="Enter title" />
      <input type="text" v-model="todo.description" placeholder="Enter description" />
      <input type="text" v-model="todo.due_date" placeholder="Enter due_date" />
      <input type="text" v-model="todo.completed" placeholder="Enter status" />
      <button type="button" @click="update">Update Todo List</button>
    </form>
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
      name: '',
      todo: {
        title: '',
        description: '',
        due_date: '',
        completed: ''
      }
    }
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
    }
  },
  async mounted() {
    console.warn("mounted")
    let user = localStorage.getItem('user info');
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({
        name: 'signUp'
      });
    }
    console.warn(this.$route.params.id);
    const result = await axios.get(`http://localhost:3000/todo/${this.$route.params.id}`);
    console.warn(result);
    this.todo = result.data; // prefill data
  }
}
</script>

<style>
</style>
