<template>
    <div>
        <ToDoList v-bind:todos="todos"></ToDoList>
        <CreateToDo v-on:add-todo="addTodo"></CreateToDo>
    </div>
</template>

<script>
    import Vue from 'vue';
    import ToDoList from './components/ToDoList';
    import CreateToDo from "@/components/CreateToDo";
    import VueToast from 'vue-toast-notification';
    import 'vue-toast-notification/dist/index.css';
    Vue.use(VueToast);
    export default {
        components: {
            ToDoList,
            CreateToDo,
        },
        data() {
            return {
                todos: [{
                    title: 'Todo A',
                    description: 'Project A',
                    date: new Date(2019, 10, 20),
                    done: false,
                }, {
                    title: 'Todo B',
                    description: 'Project B',
                    date: new Date(2019, 10, 2),
                    done: true,
                }, {
                    title: 'Todo C',
                    description: 'Project C',
                    date: new Date(2019, 11, 20),
                    done: false,
                }, {
                    title: 'Todo D',
                    description: 'Project D',
                    date: new Date(2019, 11, 31),
                    done: false,
                }],
            };
        },
        methods: {
            addTodo(newToDo) {
                this.todos.push(newToDo);
                Vue.$toast.success('Added!');
            },
        },
    };
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
