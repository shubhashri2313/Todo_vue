<template>
 
<router-view />
</template>

<script>

export default {
  name: 'App',
 
}
</script>

<style>
body{
    padding:0;
    margin:0

}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  //margin-top: 60px;
}

.logo{
    width:100px;

}
.register input, .login input ,.add input, .update input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;

}

.register button,.login button,.add button,.update button{
    width: 320px;
    height:40px;
    background-color:skyblue;

}
</style>
