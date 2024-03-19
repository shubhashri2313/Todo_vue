<template>
<img  class ="logo" src="../assets/resto_logo.jpg" />
<h1>Sign Up</h1>

<div class="register">
<input type ="text"  v-model="name" placeholder="Enter Name"/>
<input type ="Email"  v-model="email" placeholder="Enter Email"/>
<input type ="Password"  v-model="password" placeholder="Enter Password"/>
<button v-on:click="signUp">SignUp</button>
<p>
<router-link to="/login">Login
</router-link></p>
</div>  

</template>
<script>
import axios from 'axios'
export default{
    name :'SignUp',
    data(){
        return{
          name:'',
          email:'',
          password:''

        } 
    },
    methods:{
        async signUp(){
            console.warn("signup",this.name,this.email,this.password)
            let result=  await axios.post("http://localhost:3000/users",{
                name: this.name,
                email:this.email,
                password:this.password

            });
           console.warn(result);
           if(result.status==201){
               alert("sign up done")
           }
           localStorage.setItem("user info",JSON.stringify(result.data))
           this.$router.push({name:'Home'})
        }
    },
    mounted(){
        console.warn("mounted")
        let user= localStorage.getItem('user info');
        if(user){
             this.$router.push({name:'Home'}) // it will redirect to home page if user found
        }
    }

}
</script>
<style>

</style>




