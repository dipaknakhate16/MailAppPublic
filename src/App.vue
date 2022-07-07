<template>
<div class="container">
  <div class="mail-box">
    <appSidevbar :messages="messages"></appSidevbar>
    <appContent  :messages="messages"> </appContent>
  </div>
</div>
</template>

<script>
import Sidebar from "./Sidebar.vue";
import Content from "./content.vue";
import messages from "./data/messages";

export default{
  data(){
    console.log(messages[0])
    return {
    
      messages:messages
    }
    
  },
   components:{
    appSidevbar:Sidebar,
    appContent:Content
}

}

</script>