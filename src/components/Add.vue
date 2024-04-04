<template>
<div>
    <Header />
    <div class="container mt-5">
        <h1><i class="fas fa-plus-circle"></i> Add Todo List</h1>
        <form class="add mt-4">
            <div class="mb-3">
                <label for="title" class="form-label">Title</label>
                <input type="text" id="title" name="title" v-model="title" class="form-control" placeholder="Enter title" />
            </div>
            <div class="mb-3">
                <label for="description" class="form-label">Description</label>
                <input type="text" id="description" name="description" v-model="description" class="form-control" placeholder="Enter description" />
            </div>
            <div class="mb-3">
                <label for="status" class="form-label">Status</label>
                <select id="status" name="status" v-model="status" class="form-select">
            <option value="todo">Todo</option>
            <option value="in progress">In Progress</option>
            <option value="finished">Finished</option>
          </select>
            </div>
            <div class="mb-3">
                <label for="due_date" class="form-label">Due Date</label>
                <input type="date" id="due_date" name="due_date" v-model="due_date" class="form-control" placeholder="Enter due date" />
            </div>
            <button type="button" @click="add" class="btn btn-primary"><i class="fas fa-plus"></i> Add Todo List</button>
        </form>
    </div>
</div>
</template>

 
 
    
<script>
import axios from 'axios'
import Header from './Header.vue'

export default {
    name: 'Add',
    components: {
        Header
    },
    data() {
        return {

            title: '',
            description: '',
            due_date: '',
            completed: '',

        };
    },
    methods: {
        async add() {
            console.warn("add", this.title)
            let result = await axios.post("http://localhost:3000/todo", {
                title: this.title,
                description: this.description,
                due_date: this.due_date,
                completed: this.completed

            });
            if (result.status == 201) {
                this.$router.push({
                    name: 'Home'
                });

            }
            console.warn("result", result)
        }

    },
    mounted() {
        console.warn("mounted")
        let user = localStorage.getItem('user info');
        if (!user) {
            this.$router.push({
                name: 'signUp'
            }) // it will redirect to sign up page if user  not found
        }
    }

}
</script>

<style>

</style>
