<template>
  <transition name="fade">
    <div class="modal">
      <div class="content">
        
        
        <div class="header">
        <h2>Düzenle</h2>
        <button  @click="() => {this.$emit('close-modal');}" class="closeButton"> X</button>
        </div>
        
        <div class="inputFields">
          <h3>Title</h3>
          <input type="text" id="title" placeholder="Title" v-model="pusableObject.title" />

          <h3>Content</h3>
          <textarea name="" id="" cols="30" rows="10" placeholder="Content" v-model="pusableObject.body" ></textarea>
        </div>

        <button @click="updateIt">GÜNCELLE</button>
      </div>
    </div>
  </transition>
</template>


<script>
export default {
   name: "Modal",
  props: {
    tobeeditted: Object,
  },
  data(){
    return{
      pusableObject : {}
    }
  },
  methods : {
   async updateIt() {
      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var raw = JSON.stringify({
        userId: this.pusableObject.userId,
        id: this.pusableObject.id,
        title: this.pusableObject.title,
        body : this.pusableObject.body
      });

      var requestOptions = {
        method: 'PATCH',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      fetch(`https://jsonplaceholder.typicode.com/posts/${this.pusableObject.id}`, requestOptions)
        .then((response) => {
          if(response.status === 200){
            
            this.$emit('close-modal')
          }
        })
        .catch(error => console.log('error', error));
    }
  },  
  created () {
    this.pusableObject = this.tobeeditted
  }
}
</script>

<style scoped>
html,
body {
  overflow-y: hidden !important;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.modal {
  background: rgba(0, 0, 0, 0.5);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(7px);
  -webkit-backdrop-filter: blur(7px);
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 9;

  color: #32325d;
}

.content {
  width: 500px;
  height: 421px;
  background: #ffffff;
  box-shadow: 0px 15px 35px rgba(50, 50, 93, 0.1),
    0px 5px 15px rgba(0, 0, 0, 0.07);
  border-radius: 4px;
  margin: 0 auto;
  position: relative;
  top: 25vh;

  padding: 1em 1.3em;
  text-align: left;
}

.content h2 {
  
  font-weight: 400;
  font-size: 16px;
}

.content input
 {
    all: unset;
  width: 92%;
  border: 1.5px solid #CAD1D7;
  border-radius: 4px;
  padding: 6px 12px;
  
}

.content textarea{
    all: unset;
    width: 92%;
    border: 1.5px solid #CAD1D7;
    border-radius: 4px; 
    height: 102px;
    padding: 6px 12px;
}

.content h3 {
  font-size: 14px;
  font-weight: 600;
}

.content label {
  width: 500px;
  background: blue;
}

.content .inputFields {
  padding: 5px 0px;
  padding-bottom: 26px;
  border-bottom: 1px solid #e9ecef;
}

.closeButton{
    all: unset;
    cursor: pointer;
    color: #888888;
    font-weight:600;
}

.closeButton:hover{
    color: #4e4e4e;
}

.header{
    display: flex;
    flex-direction: row;
    width: 100%;
    align-content: center;
    justify-content: space-between;

    border-bottom: 1px solid #e9ecef;

}

button{
    all: unset;
  color: white;
  width: 118px;
  height: 43px;
    background: #11CDEF;
    text-align: center;
    margin-top: 24px;
  box-shadow: 0px 4px 6px rgba(50, 50, 93, 0.11),
    0px 1px 3px rgba(0, 0, 0, 0.08);
  border-radius: 4px;
  margin-right: 20px;
  font-size: 14px;
  line-height: 16px;
  letter-spacing: 0.08px;
  font-weight: bold;
  cursor: pointer;
}
</style>