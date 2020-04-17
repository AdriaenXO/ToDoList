<template>
    <div class='ui centered card'>
        <div class="content" v-show="!isEditing">
            <div class='header'>
                {{ todo.title }}
            </div>
            <div class='meta'>
                {{ todo.description }}<br/>
                <i class='calendar alternate outline icon'></i>{{ formatDate(todo.date) }}
            </div>
            <div class='extra content'>
                <span class='ui button right floated edit icon' v-on:click="showForm">
                    <i class='edit icon'></i>
                </span>
                <span class='ui button right floated trash icon' v-on:click="deleteTodo(todo)">
                    <i class='trash icon'></i>
                </span>
            </div>
        </div>
        <div class="content" v-show="isEditing">
            <div class='ui form'>
                <div class='field'>
                    <label>Title</label>
                    <input type='text' v-model="todo.title" >
                </div>
                <div class='field'>
                    <label>Description</label>
                    <input type='text' v-model="todo.description" >
                </div>
                <div class='field'>
                    <label>Date</label>
                    <datepicker v-model="todo.date"></datepicker>
                </div>
                <div class='ui two button attached buttons'>
                    <button class='ui basic blue button' v-on:click="hideForm">
                        Save
                    </button>
                </div>
            </div>
        </div>
        <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" v-on:click="uncompleteTodo(todo)">
            Completed
        </div>
        <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" v-on:click="completeTodo(todo)">
            Not completed
        </div>
    </div>
</template>

<script type="text/javascript">
    import Datepicker from 'vuejs-datepicker';
    import Vue from 'vue';
    import VueToast from 'vue-toast-notification';
    import 'vue-toast-notification/dist/index.css';

    Vue.use(VueToast);
    //import format from 'date-fns';
    export default {
        components: {
            Datepicker,
        },
        props: ['todo'],
        data() {
            return {
                isEditing: false,
            };
        },
        methods: {
            showForm() {
                this.isEditing = true;
            },
            hideForm() {
                this.isEditing = false;
                Vue.$toast.success('Changes saved.');
            },
            deleteTodo(todo) {
                this.$emit('delete-todo', todo);
            },
            completeTodo(todo) {
                this.$emit('complete-todo', todo);
            },
            uncompleteTodo(todo) {
                this.$emit('uncomplete-todo', todo);
            },
            formatDate(date) {
                return date.toDateString();
            },
        },
    };
</script>