<template>
        <button @click="openModal" class="edit">  DÜZENLE</button>
</template>


<script>
export default {
    name : 'EditButton',
    props : {
        postObj : Object
    },
    data (){
        return {
            result : []
        }
    },
    methods : {
        openModal(){
          
            this.$emit('modal-opened', this.postObj)
        }
    }
}
</script>