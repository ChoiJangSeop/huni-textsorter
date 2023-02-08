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
            memoryPassword: false,
        }
    },
    mounted() {
        this.isLogin = false;
        console.log(this.getCookie("passwordMemory"));


        if (this.getCookie("passwordMemory").length > 0) {
            this.inputPassword = this.getCookie("passwordMemory");
            this.memoryPassword = true;
        }
    },
    methods: {
        enter() {
            if (this.inputPassword === this.password) {
                this.isLogin = true;
                if (this.memoryPassword) this.setCookie("passwordMemory", this.inputPassword);
                else this.deleteCookie("passwordMemory");
            }
            else {
                this.inputPassword = "";
                alert("비밀번호 모르네? 나가 그냥");
            }
        },

        changeType(type) {
            this.type = type;
        },

        setCookie(cookieName, value) {
            document.cookie = cookieName + "=" + value;
        },

        getCookie(cookieName) {
            cookieName = cookieName + "=";
            var cookieData = document.cookie;
            var start = cookieData.indexOf(cookieName);
            var value = "";

            if (start !== -1) {
                start += cookieName.length;
                value = cookieData.substring(start, cookieData.length);
            }

            return value;
        },

        deleteCookie(cookieName) {
            document.cookie = cookieName + '=; expires=Thu, 01 Jan 1970 00:00:01 GMT;';
        },

        popUpDeveloperNote() {
            document.querySelector("#developer-note").style.display = 'block';
        },

        closeDeveloperNote() {
            document.querySelector("#developer-note").style.display = 'none';
        }
    }
}
</script>

<template >
    <div v-if="!isLogin">
        <h1>비밀번호 모르면 접속할 생각 꿈도 꾸지마<br>무료로 이용 할 생각 추어도 하지마</h1>
        <input type="password" v-model="inputPassword">
        <button style="margin-left: 7px;" @click="enter">접속</button>
        <input style="margin-left: 15px;" type="checkbox" id="memory-password" v-model="memoryPassword">
        <label style="margin-left: 1px;" for="memory-password">비밀번호 기억하기</label>
    </div>
    <div v-else>
        <h1>엔조이런너 운영자 귀여운 훈이의 텍스트 편집기</h1>
        <h5>v2.2.0</h5>
        <h5>만든이 : HUNI LOVER SEOP</h5>
        <div id="buttonList">
            <button style="margin-right: 10px;" @click="changeType(1)">아이템 순서 정렬</button>
            <button style="margin-right: 10px;" @click="changeType(2)">아이템 지급 파일 변환</button>
            <button @click="changeType(3)">아이템 주요정보 추출</button>
            <button id="developer-note-btn" href="#developer-note" @click="popUpDeveloperNote">개발자노트</button>
        </div>
        <HelloWorld v-if="type === 1"/>
        <ConvertItemForm v-if="type === 2"/>
        <ItemMainInfoExtractor v-if="type === 3"/>

        <div id="developer-note" class="pop_wrap" style="display:none;">
            <div class="pop_inner">
                <h3 class="dsc" style="font-weight: bold;">개발자 노트</h3>
                <p>v2.2.1</p>
                <p style="text-align: left;">
                    <ul>
                        <li>비밀번호 기억하기 기능 추가</li>
                        <li>아이템 순서 정렬기 다운로드 텍스트파일 UTF-16을 기본형식으로 변경</li>
                        <li>개발자 노트 추가</li>
                    </ul>
                </p>
                <p style="font-weight: bold; text-align: left; margin-left:10px; margin-top: 70px;">명훈이에게</p>
                <p style="text-align: left; margin-left: 10px;">  
                    안녕 명후나, 형이야 우리가 벌써 만난지 70일이 지났어! 시간 진짜 빠르다 ㅎㅎ<br>
                    최근에 참 여러 일들을 겪으면서 훈이를 속상하게 만들고, 슬프게 만든것 같아서 형이 미안하기도 하네.
                    나는 가끔 훈이가 다른 다양한 일들을 해봤으면 좋겠다! 이런 생각에 은근히 이런저런 말들을 했는데
                    조금은 내입장에서만 생각한게 아닌가 싶어. 형이 훈이를 이해한다는게 가끔은 형의 입장에서 훈이를 보게 되더라구...<br><br>
                    그런데 최근에 느낀거지만 형이 생각하는것보다 훈이는 더 어른스러운 사람이고, 더 생각이 많고 나를 배려하는 사람이더라고 헤헤.
                    특히, 오늘 훈이 업데이트한다고 고생하는것 보고서 훈이가 서버를 진심으로 잘 운영하기 위해 열심히 사는구나 느꼈어.
                    또 가끔 아주 아쉬운 말투로 형 운동갔다와,,, 그래 일해,,, 하는것 보면서 나도 안타깝지만 그래도 훈이가 나를 많이 배려하는구나 느껴! ㅋㅋㅋ<br><br>
                    앞으로 훈이를 더 훈이 그대로 받아들일려고, 그러는게 훈이를 그대로 사랑하는게 아닐까 싶어
                    그래도 가끔 형이 하는 조언 다아아아 훈이 위한 거니깐 너무 흘려듣지 말구,,,ㅋㅋ(너무 꼰대 같나?)
                    우리 앞으로 서로를 더 서로 그대로 더 받아들이고 이해하자. 그게 진짜 사랑하는게 아닐까 싶어<br><br>
                    형이 훈이 평생 사랑해. 월급 나오면 진짜 맛있는거 먹으러 가고. 마루이 비디오도 보고 팽자팽자 놀아보자구~ ㅋㅋㅋ<br>
                    훈아 사랑해. 앞으로 우리 서로 미안하단 말 하지 말고, 고맙다는 말만 할 수 있는 사랑하자<br><br>
                </p>
                <p style="font-weight: bold; text-align: left; margin-left:10px; margin-bottom: 10px;">훈이를 가장 사랑하는 유일한 사람이</p>
                <button type="button" class="btn_close" @click="closeDeveloperNote">닫기</button>
            </div>
        </div>
    </div>

    
</template>

<style scoped>

#developer-note-btn {
    background-color: bisque;
    margin-left: 10px;
}

#developer-note {
    background-color: azure;
    color:black;
    border: 1px solid black;
    width: 800px;
    margin-top: 100px;
    margin-left: auto;
    margin-right: auto;
}

</style>
