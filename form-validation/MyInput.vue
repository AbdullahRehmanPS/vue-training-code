<template>
    <div class="label">
        <label v-bind:for="name">
            {{ name }}
        </label>
        <div class="error">{{ error }}</div>
    </div>
    
    <!-- <input 
        v-bind:id="name"
        v-bind:value="value" 
        v-on:input="input" 
    /> -->

    <!-- <input 
        v-bind:id="name"
        v-model="value"
    /> -->

    <input 
        v-bind:id="name"
        v-bind:value="value" 
        v-bind:type="type"
        v-on:input="input" 
    />
</template>

<script>
export default {    //v-on:input="increment" is same as @input="increment" 
                    //and v-bind:value="value" is same as :value="value"
    props: {
        name: {
            type: String,
            required: true
        },
        value: {
            type: String,
            required: true
        },
        rules: {
            type: Object,
            default: {}
        },
        type: {
            type: String,
            default: 'text'
        },
        error: {
            type: String
        }
    },

    emits: ['update'],

    // data() {
    //     return {
    //         value: ''
    //     }
    // },

    // computed: {
    //     error() {
    //         if ( this.rules.required && this.value.length === 0 ) {
    //             return 'value is required.'
    //         } 
    //         if ( this.rules.min && this.value.length < this.rules.min ) {
    //             return `the min length is ${this.rules.min}.`
    //         }
    //     }
    // },

    created() {
        this.$emit('update', {
                name:  this.name.toLowerCase(),
                value: this.value,
                error: this.validate(this.value)
            })
    },

    methods: {
        input($event) {
            //this.value = $event.target.value;
            this.$emit('update', {
                name:  this.name.toLowerCase(),
                value: $event.target.value,
                error: this.validate($event.target.value)
            })
        },
        validate(value) {
            if ( this.rules.required && value.length === 0 ) {
                return 'value is required.'
            } 
            if ( this.rules.min && value.length < this.rules.min ) {
                return `the min length is ${this.rules.min}.`
            }
        }
    }
}
</script>

<style scoped>
.input {
  display: flex;
  flex-direction: column;
}
.label {
  display: flex;
  justify-content: space-between;
}
.error {
  color: red;
}
.input {
  width: 100%;
}
input {
  box-sizing: border-box;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid silver;
  margin: 2px;
  font-size: 16px;
  width: 100%;
  cursor: pointer;
}
</style>