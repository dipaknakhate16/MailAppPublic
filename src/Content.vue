<template>
<aside class="ig-side">
<div class="inbox-head">
    <h3>{{ currentView.title}}</h3>
    
</div>
    <keep-alive>
        <component :is="currentView.tag" :data="currentView.data"></component>
    </keep-alive>
</aside>
</template> 

<script>
import Inbox from './Inbox.vue';
import Sent from './Sent.vue';
import Important from './Important.vue';
import Trash from './Trash.vue';
import Viewmessage from './Viewmessage.vue';
import messages from './data/messages';
import {eventBus }from './main'
 
export default{
    props:{
        messages:{
            type:Array,
            required: true
        }
    },
    created(){
        eventBus.$on('changeView',(data)=>{
            let temp = [{
                tag:data.tag,
                title:data.title,
                data:data.data || {}
            }];
            //console.log(data.tag)
            //this.history= temp;
            this.history = temp.concat(this.history.splice(0));
            console.log("buson",this.history)
        });
    },
    data(){
        return{
            history: [
                {
                 tag:'app-inbox',
                 title: 'Inbox',
                 data:{
                    messages:null
                 }
            }]
        };
    },
    computed: {
        currentView(){
            let current= this.history[0]
            current.data.messages= this.messages
            return current;
        },
        previousView(){
            //console.log(" current view ",this.history[1])
            return typeof this.history[1] !== 'undefined' ? this.history[1] : null ;
        }
    }
,
components:{
    appInbox:Inbox,
    appSent:Sent,
    appImportant:Important,
    appTrash:Trash,
    appViewMessage:Viewmessage,

}

}
</script>