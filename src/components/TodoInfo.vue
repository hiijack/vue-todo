<template>
    <div>
        <span><a href="#" v-on:click="changeShowType('all')">所有事项</a>：{{total}}</span>
        <span><a href="#" v-on:click="changeShowType('notDone')">未完成</a>：{{notDone}}</span>
        <span><a href="#" v-on:click="changeShowType('done')">已完成</a>：{{done}}</span>
    </div>
</template>

<script>
    export default {
        name: 'todoInfo',
        props: ['list', 'showType'],
        computed: {
            total() {
                return this.list.length;
            },
            done() {
                return this.list.filter(item => {
                    return item.done;
                }).length;
            },
            notDone() {
                return this.list.filter(item => {
                    return !item.done;
                }).length;
            }
        },
        methods: {
            changeShowType(type) {
                this.$emit('changeShowType', type);
            }
        }
    }

</script>

<style scoped>
    span {
        margin: 0 5px 0 5px;
    }
    
    a {
        text-decoration: none;
        color: #42b983;
        font-weight: 600;
    }
</style>