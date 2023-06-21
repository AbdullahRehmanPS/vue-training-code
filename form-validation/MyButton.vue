<template>
    <button
        v-bind:style="{ background, color }"
        v-bind:disabled="disabled"
    >
    my button
    </button>
</template>

<script>
export default {
    props: {
        background: {
            String
        },
        color: {
            String
        },
        disabled: {
            Boolean
        }
    }
}
</script>

<style scoped>
button {
    background: none;
    color: black;
    border: none;
    padding: 10px 40px;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    margin-top: 10px;
}
button:disabled {
  opacity: 0.5;
}
button:hover {
  filter: brightness(125%);
}
</style>