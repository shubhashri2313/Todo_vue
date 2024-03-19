<template>
<Header/>
<h1>  hello user, Welcome to Update Todo List page</h1>
<form class="update">
    <input type="text" v-model="title" placeholder="Enter title" />
    <input type="text" v-model="todo.description" placeholder="Enter description" />
    <input type="text" v-model="todo.due_date" placeholder="Enter due_date" />
    <input type="text" v-model="todo.status" placeholder="Enter status" />
    <button type="button" v-on:click="update">update Todo List</button>
</form>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
 export default {
     name: 'Update',
    components:{
        Header
    },
      data() {
        return {
            todo: {
                title:'',
                description:'',
                due_date:'',
                status:''

            }
        }
    },
    methods: {
        async update() {
            console.warn("update function called",this.todo)
            let result = await axios.put("http://localhost:3000/todo/"+this.$route.params.id, {
                title: this.title,
                description: this.description,
                due_date: this.due_date,
                completed: this.completed,

            });
            if (result.status == 200) {
                this.$router.push({name: 'Home' });
               
            }
            console.warn("result",result)
        }

    },
    async mounted() {
         console.warn("mounted")
         let user = localStorage.getItem('user info');
         this.name=JSON.parse(user).name// data will store in string and then we will pass dynamically just like props
         if (!user) {
             this.$router.push({
                 name: 'signUp'
             }) // it will redirect to sign up page if user  not found
         }
         console.warn(this.$route.params.id)
         const result= await axios.get("http://localhost:3000/todo/"+ this.$route.params.id);
         console.warn(result)
         this.todo=result.data// prefill data

     }
 }
</script>

<style>

</style>
