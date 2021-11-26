<template>
<div>
  <Modal :tobeeditted="modalObject"  @close-modal="modalClose"  v-if="modalClosed"/>
    <div class="posts">

    
    <ul>
      <li v-for="post in posts" :key="post.id">
        <div>
          <div class="content">
            <span>{{ post.id }}</span> <span>{{ post.title }}</span>
          </div>

          <div class="buttons">
          <router-link :to="'/posts/'+post.id"> <button class="details">DETAY</button></router-link>
            <EditButton @modal-opened="openModal"  :postObj="post" />
            <DeleteButton @deleted="postDelete" :id="post.id" />
          </div>
        </div>
        <hr :class="'hr'+post.id" />
      </li>
    </ul>
  </div>
</div>
</template>


<script>
import DeleteButton from '../components/buttons/DeleteButton.vue'
import EditButton from '../components/buttons/EditButton.vue'
import Modal from '../components/Modal.vue'
export default {
  data() {
    return {
      posts: [],
      modalClosed : false,
      modalObject : undefined
    };
  },
  components:{
  DeleteButton,
  EditButton,
  Modal
  },
  async created() {
    //fetch api
    this.postFethcer();
   
  },
  methods: {
    async postFethcer() {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      await fetch("https://jsonplaceholder.typicode.com/posts", requestOptions)
        .then((response) => response.text())
        .then((result) => {
          this.posts = JSON.parse(result);
          this.posts = this.posts.slice(0, 6);
        })
        .catch((error) => console.log("error", error));
    },
    postDelete($event){
    

    this.posts = this.posts.filter( (post) => post.id !== $event)

    
  },
  modalClose(){
    this.modalClosed = !this.modalClosed
  },
  openModal($event){

    this.modalObject = $event
    this.modalClosed = !this.modalClosed
  }
  },
  
};
</script>

<style scoped>
a{
  text-decoration: none;
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
  padding: 1em 2em;
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



ul {
  list-style: none;
  padding: 0;
}

ul li {
  display: inline-block;
  width: 100%;
}
ul li > div {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-content: flex-start;
  width: 100%;
}

ul li div > span:first-child {
  font-weight: bold;
}

ul li div > span:last-child {
  font-weight: 400;
  margin-left: 10px;
}
ul li:first-child {
  padding-top: 41px;
}

.content {
  padding: 2px;
  position: relative;
  top: 13px;
}

.buttons button {
  all: unset;
  color: white;
  width: 99px;
  height: 43px;

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

.buttons .details {
  background: #5e72e4;
}

.buttons .delete {
  background: #fb6340;
}

.buttons .edit {
  background: #2dce89;
}

.hr6{
  opacity: 0;
}
</style>
