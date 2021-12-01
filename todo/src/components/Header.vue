<template>
    <div class="header">
        <h1 class="today">{{ time }}</h1>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            time: ""
        }
    },
    created() {
        var today = new Date();

        var month = today.getMonth() + 1;
        var date = today.getDate();

        this.time = `${month}/${date}`;
    }
}
</script>

<style scoped>
.header {
    margin-left: 50px;
    width: 0px;
}
.today {
    font-size: 100px;
}
</style>