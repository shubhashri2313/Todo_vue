<template>

<div>
    <Header />
    <div class="container mt-5">
        <h1>Hello {{ name }}, Welcome from the home page</h1>
        <table border="3px">
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Title</th>
                    <th>Description</th>
                    <th>Status</th>
                    <th>Due Date</th>
                    <th>Completed</th>
                    <th>Action</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, i) in todos" :key="i">
                    <td>{{ item.id }}</td>
                    <td>{{ item.title }}</td>
                    <td>{{ item.description }}</td>
                    <td>{{ item.status }}</td>
                    <td>{{ item.due_date }}</td>
                    <td>{{ item.completed }}</td>
                    <td>
                        <router-link :to="'/update/' + item.id" class="btn btn-primary"><i class="fas fa-edit"></i> Update</router-link>
                    </td>
                    <td>
                        <button @click="deleteItem(item.id)" class="btn btn-danger"><i class="fas fa-trash-alt"></i> Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
</template>

<script>
import axios from "axios";
import Header from "./Header.vue";

export default {

    name: "Home",
    data() {
        return {
            name: "",
            todos: [],
        };
    },
    methods: {
        async deleteItem(id) {
            if (confirm("Are you sure you want to delete this item?")) {
                try {
                    await axios.delete("http://localhost:3000/todo/" + id);
                    this.loadTodo();
                } catch (error) {
                    console.error("Error deleting item:", error);
                }
            }
        },
        async loadTodo() {
            console.warn("loading....");
            let user = localStorage.getItem("user info");
            this.name = JSON.parse(user).name;
            if (!user) {
                this.$router.push({
                    name: "signUp",
                });
            }
            try {
                let result = await axios.get("http://localhost:3000/todo");

                console.warn(result);
                this.todos = result.data;
            } catch (error) {
                console.error("Error loading todos:", error);
            }
        },
    },
    components: {
        Header,
    },
    mounted() {
        this.loadTodo();
    },

  name: "Home",
  data() {
    return {
      name: "",
      todos: [],
    };
  },
  methods: {
    async deleteItem(id) {
      if (confirm("Are you sure you want to delete this item?")) {
        try {
          await axios.delete("http://localhost:3000/todo/" + id);
          this.loadTodo();
        } catch (error) {
          console.error("Error deleting item:", error);
        }
      }
    },
    async loadTodo() {
      console.warn("loading....");
      let user = localStorage.getItem("user info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({
          name: "signUp",
        });
      }
      try {
        let result = await axios.get("http://localhost:3000/todo");
        console.warn(result);
        this.todos = result.data;
      } catch (error) {
        console.error("Error loading todos:", error);
      }
    },
  },
  components: {
    Header,
  },
  mounted() {
    this.loadTodo();
  },

};
</script>

<style>
td {

    width: 160px;

  width: 160px;

}
</style>
