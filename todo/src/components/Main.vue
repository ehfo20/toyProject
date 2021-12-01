<template>
    <div class="inputBox">
        <input type="text" v-model="input" v-on:keyup.enter="inputList" />
    </div>
    <div class="listBox">
        <span class="warningText">{{ warning }}</span>
        <ul>
            <li v-for="item in list" v-bind:key="item">
                {{ item }}
                <div class="removeBox">
                    <span class="removeButton" v-on:click="removeList(item)"><img src="../assets/tresh.png" alt="tresh" width="30" height="30"></span>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            input: "",
            list: [],
            count: localStorage.length - 1,

            warning: ""
        }
    },
    created() {
        for (var i = 0; i <= localStorage.getItem("num"); i++) {
            if (localStorage.getItem(i) != null) this.list.push(localStorage.getItem(i));
        }
    },
    methods: {
        inputList() {
            if (this.input != "") {
                for (var i = 0; i <= localStorage.getItem("num"); i++) {
                    if (localStorage.getItem(i) == this.input) {
                        this.warning = "중복된 값입니다.";
                        this.input = "";
                        return;
                    }
                }
                this.warning = "";

                if (this.count < 0) this.count = 0;

                this.list.push(this.input);

                localStorage.setItem(this.count, this.input);
                localStorage.setItem("num", this.count);
                this.count++;
                this.input = "";
            }
            else {
                this.warning = "잘못된 값입니다.";
            }
        },
        removeList(item) {
            var i;

            for (i = 0; i < this.count; i++) {
                if (localStorage.getItem(i) == item) {
                    localStorage.removeItem(i);
                    break;
                }
            }
            for (i = 0; i < this.list.length; i++) {
                if (this.list[i] == item) {
                    this.list.splice(i, 1);
                   break;
                }
            }

            console.log(localStorage, this.list);
        }
    }
}
</script>

<style scoped>
.inputBox {
    margin-top: 100px;
    margin-left: 60px;

    width: 582px;
    height: 50px;
    border: 2px solid #19ce60;
    border-radius: 2px;
}
.inputBox input {
    width: 100%;
    height: 100%;
    padding: 0px;
    border-width: 0px;

    font-size: 18px;
    font-weight: 700;

    outline: none;
}
.warningText {
    margin-left: -495px;

    color: #de4343;
}
.listBox li {
    margin: 0.5rem 0;
    margin-left: 20px;

    display: flex;
    
    width: 700px;
    height: 50px;
    line-height: 50px;
    padding: 0 0.9rem;
    background-color: #EAEAEA;
    border-radius: 2px;
}
.removeBox {
    margin-top: 10px;
    margin-left: auto;

    width: 8.5rem;
    height: 30px;
    line-height: 30px;
    background-color: white;
    border-radius: 10000px;
}
.removeButton {
    display: block;
    color: #de4343;
}
</style>