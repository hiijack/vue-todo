<template>
    <div>
        <ul>
            <li v-for="ls in displayList" v-bind:class='{done: ls.done}'>
                <input type="checkbox" class="checkbox" v-model="ls.done">
                <label v-on:dblclick="edit(ls)" v-bind:class="{hidden: ls.edited}">{{ls.text}}</label>
                <input type="text" class="edit" v-focus v-bind:class="{show: ls.edited}" v-model="ls.text" v-on:blur="update(ls)">
                <input type="button" value="x" class="delete" v-on:click="deleteTodo(ls.key)">
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'todoList',
        props: ['list', 'showType'],
        computed: {
            displayList() {
                if (this.showType == 'done') {
                    return this.list.filter(item => {
                        return item.done;
                    });
                } else if (this.showType == 'notDone') {
                    return this.list.filter(item => {
                        return !item.done;
                    })
                } else {
                    return this.list;
                }
            }
        },
        methods: {
            deleteTodo(key) {
                this.$emit('deleteTodo', key);
            },
            edit(ls) {
                ls.edited = true;
            },
            update(ls) {
                ls.edited = false;
            }
        },
        directives: {
            focus: {
                update: function (el) {
                    el.focus()
                }
            }
        }
    }

</script>

<style scoped>
    ul {
        width: 90%;
        padding: 0;
        margin: 0;
        list-style: none;
    }
    
    li {
        height: 28px;
        margin: 3% 0 0 10%;
        text-align: left;
    }
    
    .checkbox {
        margin: 5px;
    }
    
    .done {
        text-decoration: line-through;
        color: #ccc;
    }
    
    .delete {
        float: right;
        background-color: #ccc;
        border-color: #ccc;
        border-style: solid;
    }
    
    .edit {
        margin-left: 10px;
        height: 20px;
        font-size: 18px;
        display: none;
        width:70%;
    }
    
    .show {
        display: inline-block;
    }
    
    .hidden {
        display: none;
    }
</style>