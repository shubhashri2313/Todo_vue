<template>
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
         
                title:'',
                description:'',
                due_date:'',
                completed:'',

            
        };
    },
    methods: {
        async add() {
            console.warn("add",this.title)
            let result = await axios.post("http://localhost:3000/todo",{
                title: this.title,
                description: this.description,
                due_date: this.due_date,
                completed: this.completed

            });
            if (result.status == 201) {
                this.$router.push({name: 'Home' });
               
            }
            console.warn("result",result)
        }

    },
    mounted() {
        console.warn("mounted")
        let user = localStorage.getItem('user info');
        if (!user) {
            this.$router.push({ name: 'signUp' }) // it will redirect to sign up page if user  not found
        }
    }

}
</script>

<style>

</style>
