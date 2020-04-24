<template>
    <div class="right-container">
        <div class="input-container">
            <div class="tools-bar">
                <font-awesome-icon
                    :icon="['far', 'grin']"
                    width="2em"
                    fixed-width
                    @click="send('查询分值')"
                    :class="['tools-icon', muted ? 'disable' : '']"
                />&nbsp;&nbsp;
                <font-awesome-icon
                    :icon="['fab', 'docker']"
                    width="2em"
                    @click="send('获取环境')"
                    :class="['tools-icon', muted ? 'disable' : '']"
                />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["talkList", "enabled", "avatar", "title", "muted"],
    data() {
        return {
            message: "",
            position: 0
        };
    },
    methods: {
        send(msg = this.message) {
            if (msg === "" || this.muted) return;
            this.talkList.push({
                avatar: "../../static/images/avatar.jpg",
                text: msg,
                admin: 0
            });
            this.$emit("send_msg", msg);
            this.message = "";
            this.$refs.scr.click();
        },
        recv(msg, role = 1) {
            this.talkList.push({
                avatar: this.avatar,
                text: msg,
                admin: role
            });
        }
    },
    mounted() {
        if (this.$refs.textarea != undefined) {
            this.$refs.textarea.focus();
        }
    },
    updated() {
        if (this.$refs.textarea != undefined) {
            this.$refs.textarea.focus();
        }
    }
};
</script>

<style>
.avatar img {
    height: 100%;
    width: 100%;
}
.text div {
    margin: 0;
    text-align: left;
    line-height: 20px;
}
.right-container {
    height: 100%;
    width: 600px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    background: #ffffff;
}
.input-container {
    height: 170px;
    width: 100%;
    box-sizing: border-box;
    border-top: 1px solid rgb(245, 245, 248);
    background: #ffffff;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
.input-container .tools-bar {
    height: 30px;
    width: 100%;
    box-sizing: border-box;
    padding: 0 20px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
.input-container textarea {
    height: 140px;
    width: 100%;
    border: none;
    outline: none;
    box-sizing: border-box;
    padding: 10px;
    resize: none;
    background: #ffffff;
}
.input-container textarea:disabled {
    cursor: not-allowed;
    background: #ffffff;
}
</style>
