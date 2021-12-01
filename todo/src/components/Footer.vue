<template>
    <div class="clearBox">
        <span class="clearButton" v-on:click="clear">Clear</span>
    </div>
</template>

<script>
export default {
    methods: {
        clear() {
            localStorage.clear();
            location.reload();
        }
    }
}
</script>

<style scoped>
.clearBox {
    margin-left: 60px;

    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: greenyellow;
    border-radius: 2px;
}
.clearButton {
    display: block;
}
</style>