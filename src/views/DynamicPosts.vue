<template>
  <div class="DynamicPosts">
    
   
      <div class="posts">
    
  

    <div class="post">
          <h1>{{postDetails.title}}</h1>
          <p>{{postDetails.body}}</p>

          <router-link :to="'/profile/'+userDetails.id">{{userDetails.name}}</router-link>
    </div>
    
    
  </div>
  </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'DynamicPosts',
  data (){
      return{
          postDetails : [],
          userDetails : []
      }
  },
 async created(){
     await this.getPostDetails()

    console.log(`${this.postDetails.userId} | ${this.userDetails.id}`)
  
  },
  methods:{
      async getPostDetails(){
          var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/json");


            var requestOptions = {
            method: 'GET',
            headers: myHeaders,
            redirect: 'follow'
            };

            await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`, requestOptions)
            .then(response => response.text())
            .then(result => {
                this.postDetails = JSON.parse(result)
            })
            .catch(error => console.log('error', error));

            await this.getUserDetails()
      },
         async getUserDetails(){

               var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/json");


            var requestOptions = {
            method: 'GET',
            headers: myHeaders,
            redirect: 'follow'
            };

            await fetch(`https://jsonplaceholder.typicode.com/users/${this.postDetails.userId}`, requestOptions)
            .then(response => response.text())
            .then(result => {
               this.userDetails = JSON.parse(result)
               
            })
            .catch(error => console.log('error', error));

          }
  }
  
}
</script>


<style scoped>
a{
    color : #32325d;
    font-weight: bold;
    font-size: 16px;
    
}
.posts {
  width: min(78%, 90%);
  position: relative;
  top: -380px;
  min-height: 631px;
  background: #ffffff;
  box-shadow: 0px 15px 35px rgba(50, 50, 93, 0.1),
    0px 5px 15px rgba(0, 0, 0, 0.07);
  border-radius: 4px;
  padding: 5em 2em;
  margin: 0 auto;
  color: #32325d;

  font-size: 14px;
  line-height: 16px;
 
  height: auto;
}

hr {
  margin: 30px auto;
  border: none;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.posts .post h1{
    text-align: center;
    text-transform: capitalize;
}

.posts .post p{
    text-align: left;
    padding-top: 25px;
}

.posts .post p::first-letter {
  font-weight: bold;
  font-size: 18px;
  text-transform: capitalize;
}
</style>