<template>
<div class="nav">

<router-link to="/">Home</router-link>
<router-link to="add">Add</router-link>

<a v-on:click="logout">Logout</a>
</div>
</template>

<script>
export default{
    name:'Header',

    methods:{
       logout()
       {
           console.warn("Logout");
          
       }
    //     {
    //         //console.log("logout")
    //         localStorage.clear()
    //         this.$router.push(name:"Login")
    //     }
    
     }
}

</script>


<style>
.nav{
    background-color:#2305;
    overflow:hidden
}
.nav a{
    float:left;
    color:black;
    text-align:center;
    padding:16px 14px;
    text-decoration:none;
    font-size:16px;
    margin-right:4px
}
.nav a:hover{
    background-color:black;
    color:orange;
}
</style>