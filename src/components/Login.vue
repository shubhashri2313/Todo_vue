<template>
<img class="logo" src="../assets/resto_logo.jpg" />
<h1>Login</h1>
<div class="login">

    <input type="Email" v-model="email" placeholder="Enter Email" />
    <input type="Password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="login">Login</button>
    <p>
        <router-link to="/signUp">SignUp</router-link>
    </p>
</div>
</template>

    <script>
import axios from 'axios'
export default {
    name: "Login",
    data(){
        return{
            email:'',
            password:''
        }
    },
    methods:{
         async login(){
            alert("you have loged in ")
            console.warn(this.email,this.password)
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`);
            console.warn(result)
             if(result.status==200 && result.data.length > 0){
               alert("sign up done")
           }
           localStorage.setItem("user info",JSON.stringify(result.data[0])); //result.data
           this.$router.push({name:'Home'})
        }

    },
    mounted(){
        console.warn("mounted")
        let user= localStorage.getItem('user info');
        if(user){
             this.$router.push({name:'Home'}) // it will redirect to home page if user login  found
        }
    }
}
</script>

    <style>

</style>
