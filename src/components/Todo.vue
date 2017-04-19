<template>
    <div>
        <form id="todoform">
            <div class="todobox">
                <input class="todo" type="text" v-model="todoText" placeholder="待办事项"/>
                <input class="addbutton" v-on:click.prevent="add" type="submit" value="添加"/>
            </div>
        </form>
        <todoInfo v-bind:list="list" v-on:changeShowType="changeShowType"/>
        <todoList v-bind:list="list" v-bind:showType="showType" v-on:deleteTodo="deleteTodo"/>
    </div>
</template>

<script>
import TodoList from './TodoList'
import TodoInfo from './TodoInfo'

export default {
    name: 'todo',
    components: {
        TodoList, TodoInfo
    },
    data() {
        return {
            todoText: '',
            list: [],
            showType: 'all'
        }
    },
    methods: {
        add() {
            if (this.todoText == '') {
                return;
            }

            let todo = {
                key: Date.now(),
                text: this.todoText,
                done: false,
                edited: false
            }
            let arr = [];
            arr.push(todo);
            this.list = this.list.concat(arr);  
            this.todoText = '';
        },
        deleteTodo(key) {
            this.list = this.list.filter(item => {
                return item.key != key;
            });
        },
        changeShowType(type) {
            this.showType = type;
        }
    }
}
</script>

<style scoped>
.addbutton {
    color: #fff;
    height: 41px;
    width: 20%;
    margin: -1px;
    border-color: #42b983;
    background-color: #42b983;
    border-style: solid;
    border-width: 10px;
    float: right;
}
.todobox {
    display: inline-block;
    border-width: 1px;
    border-style: solid;
    border-color: #ccc;
    width: 85%;
}
.todo {
    float: left;
    width: 70%;
    height: 35px;
    margin: 3px 1px 0 15px;
    padding: 0 10px 0 0;
    font-size: 16px;
    outline: none;
    border: 0;
    box-sizing: content-box;
}
</style>
