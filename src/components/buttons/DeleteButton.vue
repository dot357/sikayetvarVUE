<template>
    <button @click="deleted" class="delete">  SİL</button>
    
</template>

<script>


export default {
    name : 'DeleteButton',
    props : {
        id : Number
    },
    data (){
        return {
            result : []
        }
    },
    components : {
    
    },
    methods : {
        deleted(){
         
            let accepted = confirm('Gönderiyi silmek istediğinize emin misiniz?')

            if(accepted){
                var requestOptions = {
            method: 'DELETE',
            redirect: 'follow'
            };

            fetch(`https://jsonplaceholder.typicode.com/posts/${this.id}`, requestOptions)
            .then(response => {
                
                if(response.status) this.$emit('deleted', this.id)
                return response.text()
            })
            }
           


        }
    }
}
</script>