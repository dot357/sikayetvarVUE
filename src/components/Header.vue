<template>
    <header>

        <nav>
         
            <router-link to="/"><img src="../assets/logo.png" alt="asd"></router-link> 
            <router-link to="/posts">Posts</router-link>
         
            <router-link to="#"><button>Login</button></router-link>
            
        </nav>

    </header>
</template>

<script>
export default {
    name : 'Header',

    created(){
      
    }
    
}
</script>


<style scoped>
header{
  /* background: linear-gradient(340.03deg, #8DDAD5 8.42%, #00CDAC 91.45%); */
  background-image: url(../assets/bg.png);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;


    user-drag: none;
    -webkit-user-drag: none;
    user-select: none;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;

    height: 550px;

    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: flex-start;
    padding-top:35px;
    clip-path: polygon(0 0, 100% 0, 100% 94%, 0 100%);
}

nav{
    display: flex;
    width: min(80%, 90%);
  
    margin: 0 auto;

    display: flex;
    flex-direction: row;

    align-content: flex-start;
    z-index: 1;

    
}
nav a:first-child{

    
}
nav a {
    display: flex;
    justify-content: center;
    align-content: center;
}
nav a:nth-child(2){
    padding-top: 5px;
    margin-left: 50.44px;
}
nav a:last-child{
    margin-left: auto;
 
}
nav a{
    all: unset;
    color: white;
    cursor: pointer;
}
nav button{
    all: unset;
    color: #5E72E4;
    width: 99px;
    height: 43px;
    background: #FFFFFF;
    box-shadow: 0px 4px 6px rgba(50, 50, 93, 0.11), 0px 1px 3px rgba(0, 0, 0, 0.08);
    border-radius: 4px;
}



</style>