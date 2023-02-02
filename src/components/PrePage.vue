<script>
import HelloWorld from './HelloWorld.vue';
export default {
    components: { HelloWorld },
    data() {
        return {
            inputPassword: "",
            password: "rlaaudgns0915",
            isLogin: false,
        }
    },

    mounted() {
        this.isLogin = false;
    },

    methods: {
        enter() {
            if (this.inputPassword === this.password) this.isLogin = true;
            else {
                this.inputPassword = "";
                alert("비밀번호를 모르면 나가시오");
            }
        }
    }
}
</script>

<template>
    <div v-if="!isLogin">
        <h1>비밀번호 모르면 모하는덴지 안알려줌 ㅡㅡ</h1>
        <input type="text" v-model="inputPassword">
        <button @click="enter">접속</button>
    </div>
    <div v-else>
        <HelloWorld/>
    </div>
</template>


