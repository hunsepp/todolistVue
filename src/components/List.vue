<template>
<div>
    <v-card
        class="pa-3 mb-3"
        :class="{'done':list.status==='done'}"
        v-for="(list, index) in todoList"
        :key="index"
    >
        <p>{{list.memo}}</p>

        <v-btn 
            v-if="list.status ==='created'"
            @click="$emit('statusControl', index, 'done')" 
            fab flat small color="green">
        완료
        </v-btn>
        <v-btn 
            v-else
            @click="$emit('statusControl', index, 'created')" 
            fab flat small color="blue">
        부활
        </v-btn>
        <v-btn 
            @click="$emit('listDelete',index)" 
            fab flat small color="red" >
            제거</v-btn>
        <v-btn
            @click='listEdit(list.memo, index)'
            v-if="list.status ==='created'"
            fab flat small color="yellow">
            수정</v-btn>
    </v-card>
    <!-- props 사용 -->
</div>

</template>
<script>
import {eventBus} from "../main"
export default {
    props:["todoList"],
    methods:{
        listEdit(memo,index){
            eventBus.listEdit(memo,index)
        }
    }
}
</script>
<style scoped>
/* 여기서 scoped 를 적고, class나id를 써도 이 list.vue 파일에만 적용되고 다른 파일엔 적용 안된다. */
.done{
    background-color: rgba(0,0,0,0.1);
}
.done p {
    text-decoration: line-through;
    color: rgba(0,0,0,0.5);
}
</style>