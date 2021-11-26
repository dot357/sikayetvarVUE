<template>
   

     <div class="posts">
    
  
    
    <div class="details">
        <h1>{{userDetails.name}}</h1>
        <span>{{userDetails.address.city}}</span>
        <ul class="details">
            <li><span>Username</span> {{userDetails.username}}</li>
            <li><span>Email</span> <a :href="'mailto:'+userDetails.email">{{userDetails.email}}</a></li>
            <li><span>Phone</span> {{userDetails.phone}}</li>
            <li><span>Website</span> {{userDetails.website}}</li>
            <li><span>Company</span> {{userDetails.company.name}}</li>
        </ul>
    </div>
  

    <div class="map">

    <iframe :src="userAddress" frameborder="0"></iframe>
    </div>
    
  </div>

</template>


<script>
export default {
    name : 'DynamicProfile',
    data (){
        return {
            userDetails : [],
            userAddress : undefined
        }
    },
    async created(){
       await this.getUserDetails()
       console.log(this.userDetails);
    },
    methods : {
        async getUserDetails(){

               var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/json");


            var requestOptions = {
            method: 'GET',
            headers: myHeaders,
            redirect: 'follow'
            };

            await fetch(`https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`, requestOptions)
            .then(response => response.text())
            .then(result => {
               this.userDetails = JSON.parse(result)

               this.userAddress = `https://www.openstreetmap.org/export/embed.html?bbox=81.10939979553224%2C-37.33863648417354%2C81.1897373199463%2C-37.29317426435304&amp;layer=mapnik" style="border: 1px solid black"></iframe><br/><small><a href="https://www.openstreetmap.org/#map=14/${this.userDetails.address.geo.lat}/${this.userDetails.address.geo.lng}`
               
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

  display: flex;
  flex-direction: row;
  gap: 60px;
}


.posts  div {
    width: 100%;
    text-align: left;
}
iframe{
    width: 100%;
    height: 338px;
}

.posts h1{
    font-weight: 400;
    font-size: 28px;
    line-break: 38,13px;
}
.posts > span{
    margin-bottom: 30px;
}
.posts span{
    font-size: 16px;
    line-height: 18,75px;
    font-weight: 300;
    margin: 0;
    margin-top: 5px;
     
}

.posts ul {
    list-style: none;
    padding: 0;
}

.posts ul span{
    color: #ADB5BD;
    display: inline-block;
    font-weight: 400;
    width: calc( 69px + 25px);
   
 
}

.posts ul li {
    font-weight: 600;
    letter-spacing: 0.11px;
    line-height: 136%;
}

.posts ul  a{
  all: unset;
}
</style>
