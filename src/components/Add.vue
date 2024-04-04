<template>
<<<<<<< HEAD
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

 
 
    
=======
<Header/>
<h1> hello user, Welcome to Add Todo List page</h1>
<form class="add">
    <input type="text"  name ="title" v-model="title" placeholder="Enter title" />
    <input type="text"  name ="description" v-model="description" placeholder="Enter description" />
    <input type="text"  name ="due_date" v-model="due_date" placeholder="Enter due_date" />
    <input type="text"  name ="completed" v-model="completed" placeholder="Enter status" />
    <button type="button" v-on:click="add">Add Todo List</button>
</form>
</template>

>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
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
<<<<<<< HEAD

            title: '',
            description: '',
            due_date: '',
            completed: '',

=======
         
                title:'',
                description:'',
                due_date:'',
                completed:'',

            
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
        };
    },
    methods: {
        async add() {
<<<<<<< HEAD
            console.warn("add", this.title)
            let result = await axios.post("http://localhost:3000/todo", {
=======
            console.warn("add",this.title)
            let result = await axios.post("http://localhost:3000/todo",{
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
                title: this.title,
                description: this.description,
                due_date: this.due_date,
                completed: this.completed

            });
            if (result.status == 201) {
<<<<<<< HEAD
                this.$router.push({
                    name: 'Home'
                });

            }
            console.warn("result", result)
=======
                this.$router.push({name: 'Home' });
               
            }
            console.warn("result",result)
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
        }

    },
    mounted() {
        console.warn("mounted")
        let user = localStorage.getItem('user info');
        if (!user) {
<<<<<<< HEAD
            this.$router.push({
                name: 'signUp'
            }) // it will redirect to sign up page if user  not found
=======
            this.$router.push({ name: 'signUp' }) // it will redirect to sign up page if user  not found
>>>>>>> 8542104888eab346a4873fca3487a3e2bf7ac09c
        }
    }

}
</script>

<style>

</style>
