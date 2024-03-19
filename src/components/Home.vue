<template>
<Header/>
<h1> Hello {{name}},Welcome from home page </h1>
<table border=3px>
    <tr>
        <td>Id</td>
        <td>Title</td>
        <td>Description</td>
        <td>Due_Date</td>
        <td>Status</td>
        <td>Action1</td>
        <td>Action2</td>
    </tr>

    <tr v-for=" item in todos" :key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.title}}</td>
        <td>{{item.description}}</td>
        <td>{{item.due_date}}</td>
        <td>{{item.completed}}</t d>
        <td>
            <router-link :to="'/update/'+item.id">Update</router-link>
        </td>
        <button v-on:click="delete(item.id)">Delete</button>

    </tr>
</table>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name: 'Home',
    data() {
        return {
            name:'',
            todos:[]

        }
    },
    methods: {
        async delete() {
            console.warn(id)
            let result = await axios.delete("http://localhost:3000/todo/" + id)
            if (result.status == 200) {

                this.loadTodo() // update the list when we delete record
            }

        },
        async loadTodo() {
            console.warn("loading....")
            let user = localStorage.getItem('user info');
            this.name = JSON.parse(user).name // data will store in string and then we will pass dynamically just like props
            if (!user) {
                this.$router.push({
                    name: 'signUp'
                }) // it will redirect to sign up page if user  not found
            }
            let result = await axios.get("http://localhost:3000/todo");
            console.warn(result)
            this.todos = result.data // to get the list when page reloads

        }

    },
    components: {
        Header
    },
    mounted() {
        this.loadTodo()
    }

}
</script>

<style>
td {
    width: 160px;
}
</style>
