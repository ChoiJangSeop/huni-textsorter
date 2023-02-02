<script>
export default {
    data() {
        return {
            comments: [],
            commentNum: 0,
            inputComment: {
                id: "",
                writer: "",
                msg: "",
            }
        }
    },

    methods: {
        sendComment() {
            if (this.inputComment.writer.length === 1 && this.inputComment.msg.length > 0) {
                this.inputComment.id = this.commentNum++;
                this.comments.push(this.inputComment);
            } else {
                alert("글쓴이를 지정하고 댓글을 입력하세요");
            }

            this.inputComment.id = "";
            this.inputComment.writer = "";
            this.inputComment.msg = "";

        }
    }
    
}
</script>

<template>
    <div id="commentInput">
        <select id="writer-select" v-model="inputComment.writer">
            <option :value="훈">훈</option>
            <option :value="썹">썹</option>
        </select>
        <input id="commentWriting" type="text" v-model="inputComment.msg" placeholder="댓글">
        <button @click="sendComment()">보내기</button>
    </div>
    <div v-for="comment in comments.reverse()" :key="comment.id">
        {{ comment.writer }} : {{ comment.msg }}<br>
        --------------------
    </div>
</template>

<style scope>
#writer-select {
    margin-right: 8px;
}

#commentInput {
    margin-top: 60px;
}

#commentWriting {
    margin-right: 8px;
    width: 900px;
}

</style>