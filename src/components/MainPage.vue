<script>
import HelloWorld from './HelloWorld.vue';
import ConvertItemForm from './CovertItemForm.vue';
import ItemMainInfoExtractor from './ItemMainInfoExtractor.vue';
export default {
    components: { HelloWorld, ConvertItemForm, ItemMainInfoExtractor },
    data() {
        return {
            inputPassword: "",
            password: "hunloveseop",
            isLogin: false,
            type: 0,
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
                alert("비밀번호 모르네? 나가 그냥");
            }
        },

        changeType(type) {
            this.type = type;
        }
    }
}
</script>

<template >
    <div v-if="!isLogin">
        <h1>비밀번호 모르면 접속할 생각 꿈도 꾸지마<br>무료로 이용 할 생각 추어도 하지마</h1>
        <input type="text" v-model="inputPassword">
        <button @click="enter">접속</button>
    </div>
    <div v-else>
        <h1>엔조이런너 운영자 귀여운 훈이의 텍스트 편집기</h1>
        <h5>v2.1.0</h5>
        <h5>만든이 : HUNI LOVER SEOP</h5>
        <div id="buttonList">
            <button style="margin-right: 10px;" @click="changeType(1)">아이템 순서 정렬</button>
            <button style="margin-right: 10px;" @click="changeType(2)">아이템 지급 파일 변환</button>
            <button @click="changeType(3)">아이템 주요정보 추출</button>
        </div>
        <HelloWorld v-if="type === 1"/>
        <ConvertItemForm v-if="type === 2"/>
        <ItemMainInfoExtractor v-if="type === 3"/>
    </div>
</template>
