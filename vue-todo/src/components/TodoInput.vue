<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->

    <span class="addContainer" v-on:click="addTodo">
    <i class="fas fa-plus addBtn"></i>
    </span>


    <Modal v-if="showModal" @close="showModal = false">
        <!--
            you can use custom content here to overwrite
            default content
        -->
        <h3 slot="header">
            잠깐!
            <i class="closeModalBtn fas fa-times" v-on:click="showModal = false"></i>
        </h3>
        
        <div slot="body">
            할 일을 입력해주세요~
        </div>
        
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false,
        }
    },
    methods: {
        addTodo() {
            if(this.newTodoItem !== '') {
                // this.$emit('이벤트이름', 인자1, 인자2)
                this.$store.commit('addOneItem', this.newTodoItem.trim()); 
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        Modal
    }
}
</script>

<style>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #545a58;
}
</style>