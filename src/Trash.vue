<template>
<div class="index-box">
    <appMessages :messages="trashMessages"></appMessages>
</div>
</template>

<script>
import Messages from './Messages.vue'
export default{
    props:{
        data:{
            type:Object,
            required:true
        }
    },
    computed:{
        trashMessages(){
                return this.data.messages.filter(function(message){
                    return message.isDeleted === true;
                });
            }
    },
    components:{
        appMessages:Messages
    }
    
}
</script>