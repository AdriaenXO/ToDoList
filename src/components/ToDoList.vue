<template>
    <div>
        <ToDo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-on:uncomplete-todo="uncompleteTodo" v-for="(todo, i) in todos" v-bind:todo="todo" v-bind:key="'todo' + i"></ToDo>
    </div>
</template>

<script>
    import ToDo from "@/components/ToDo";
    import Vue from 'vue';
    import VueToast from 'vue-toast-notification';
    import 'vue-toast-notification/dist/index.css';

    Vue.use(VueToast);
    export default {
        name: "ToDoList",
        props: ['todos'],
        components: {
            ToDo,
        },
        methods: {
            deleteTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos.splice(todoIndex, 1);
                Vue.$toast.success('Removed.');
            },
            completeTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos[todoIndex].done = true;
                Vue.$toast.success('Marked as complete.');
            },
            uncompleteTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos[todoIndex].done = false;
                Vue.$toast.success('Marked as not complete.');
            },
        },
    }
</script>

<style scoped>

</style>