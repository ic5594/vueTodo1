/* eslint-disable vue/valid-v-slot */
<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what yo have to do" 
        v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <Modal v-if="showModal" @close="showModal = false">
            <h3>경고</h3>
            <span @click="showModal = false">
                할 일을 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </Modal>
    </div>
</template>
<script>
import Modal from './common/Modal.vue'
export default {
    components:{
        "Modal":Modal
    },
    data(){
        return{
            newTodoit:'',
            showModal:false
        }
    },
    methods:{
        addTodo(){
            if(this.newTodoItem !== ""){
                var value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo',value)
                this.clearInput();
            }
            else{
                this.showModal =!this.showModal
            }
        },
        clearInput(){
            this.newTodoItem ='';
        }
    }
}
</script>
<style scoped>
input:focus{
    outline: none;
}
.inputBox{
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style:none;
    font-size:0.7rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color:white;
    vertical-align: middle;
}
</style>