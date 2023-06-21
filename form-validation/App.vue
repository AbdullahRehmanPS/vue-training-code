<template>
    <form
        v-on:submit.prevent="submit"
    >
        <my-input 
            name="Username"
            v-bind:rules="{ required: true, min: 5}"
            v-bind:value="username.value"
            v-bind:error="username.error"
            v-on:update="update"
        />

        <my-input 
            name="Password"
            v-bind:rules="{ required: true, min: 10}"
            v-bind:value="password.value"
            v-bind:error="password.error"
            type="password"
            v-on:update="update"
        />

        <my-button 
            background="blue"
            color="white"
            v-bind:disabled="!valid"
        />
    </form>
</template>

<script>
import MyButton from './MyButton.vue';
import MyInput from './MyInput.vue';

export default {
    components: {
        MyButton,
        MyInput
    },
    data() {
        return {
            //valid: true,
            username: {
                value: 'user',
                error: ''
            },
            password: {
                value: 'pass',
                error: ''
            }
        }
    },
    methods: {
        update({ name, value, error }) {
            //this.username.value = value;
            this[name].value = value;
            this[name].error = error;
        },
        submit() {
            //$event.preventDefault()
            console.log('event form')
        }
    } ,
    computed: {
       valid() {
        return (
            !this.username.error &&
            !this.password.error
        )
       } 
    }  
}
</script>

<style>
#wrapper {
  display: flex;
  justify-content: center;
  margin-top: 200px;
}
body {
  font-family: Arial;
}
form {
  max-width: 400px;
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>