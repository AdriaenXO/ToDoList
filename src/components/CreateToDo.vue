<template>
    <div class='ui basic content center aligned segment'>
        <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
            <i class='plus icon'></i>
        </button>
        <div class='ui centered card' v-show="isCreating">
            <div class='content'>
                <div class='ui form'>
                    <div class='field'>
                        <label>Title</label>
                        <input v-model="titleText" type='text' ref='title' defaultValue="">
                    </div>
                    <div class='field'>
                        <label>Description</label>
                        <input v-model="description" type='text' ref='description' defaultValue="">
                    </div>
                    <div class='field'>
                        <label>Date</label>
                        <datepicker v-model="date" ref="date"></datepicker>
                    </div>
                    <div class='ui two button attached buttons'>
                        <button class='ui basic blue button' v-on:click="sendForm">
                            Create
                        </button>
                        <button class='ui basic red button' v-on:click="closeForm">
                            Close
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Datepicker from 'vuejs-datepicker';
    import Vue from 'vue';
    import VueToast from 'vue-toast-notification';
    import 'vue-toast-notification/dist/index.css';

    Vue.use(VueToast);
    export default {
        components: {
            Datepicker,
        },
        data() {
            return {
                titleText: '',
                description: '',
                date: null,
                isCreating: false,
            };
        },
        methods: {
            openForm() {
                this.isCreating = true;
            },
            closeForm() {
                this.titleText = '';
                this.description = '';
                this.date = new Date();
                this.isCreating = false;
            },
            sendForm() {
                if (this.titleText.length > 0 && this.description.length > 0 && this.date != null) {
                    const title = this.titleText;
                    const description = this.description;
                    const date = this.date;
                    this.$emit('add-todo', {
                        title,
                        description,
                        date,
                        done: false,
                    });
                    this.titleText = '';
                    this.description = '';
                    this.date = new Date();
                    this.isCreating = false;
                }
                else {
                    Vue.$toast.error('Both title, description and date cannot be null.');
                }
            },
        },
    };
</script>