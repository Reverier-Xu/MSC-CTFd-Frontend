<template>
    <div class="right-container">
        <!-- 顶部显示回话标题 -->
        <div class="title-container">{{title}}</div>
        <!-- 聊天信息主体 -->
        <div class="info-container">
            <a
                ref="scr"
                class="scroller"
                href="#bottom"
                v-smooth-scroll="{duration: 1000, container: '.info-container'}"
            ></a>
            <div
                v-for="(item, index) in talkList"
                :key="index"
                :class="[item.admin != 0 ? '' : 'mine','info-item']"
            >
                <div class="avatar">
                    <img :src="item.admin != 0 ? 'static/images/xdmsc.png' : 'static/images/user.png'" />
                </div>
                <div class="text-container">
                    <vue-simple-markdown :source="item.text" class="text"></vue-simple-markdown>
                </div>
            </div>
            <span id="bottom"></span>
        </div>
        <!-- 输入框主体 -->
        <div class="input-container">
            <div class="tools-bar">
                <font-awesome-icon
                    :icon="['far', 'grin']"
                    width="2em"
                    fixed-width
                    @click="send('查询分值')"
                    :class="['tools-icon', muted ? 'disable' : '']"
                />&nbsp;<div @click="send()" class="submitButton">send</div>
            </div>
            <textarea
                v-if="!muted"
                placeholder="在这里写你的答案哦~只能提交一次"
                v-model="message"
                ref="textarea"
            ></textarea>
            <textarea v-if="muted" disabled placeholder="你已经回答过了..."></textarea>
        </div>
    </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import {
    faPlayCircle,
    faStopCircle,
    faClock,
    faRedoAlt
} from "@fortawesome/free-solid-svg-icons";
import { faGrin } from "@fortawesome/free-regular-svg-icons";
import { faDocker } from "@fortawesome/free-brands-svg-icons";

library.add(faPlayCircle, faStopCircle, faClock, faGrin, faDocker, faRedoAlt);
export default {
    props: ["talkList", "avatar", "title", "muted"],
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
                text: msg,
                admin: 0
            });
            this.$emit("send_msg", msg);
            this.message = "";
            this.$refs.scr.click();
        },
        recv(msg, role = 1) {
            this.talkList.push({
                text: msg,
                admin: role
            });
            this.$refs.scr.click();
        }
    }
};
</script>

<style>
.drawer {
    width: 20px;
    height: 20px;
    align-content: center;
}
.menu-open {
    display: none;
}

.avatar img {
    height: 100%;
    width: 100%;
}
.text div {
    margin: 0;
    text-align: left;
    line-height: 20px;
}
.text .name {
    font-size: 16px;
    width: 100%;
    white-space: nowrap;
}
.right-container {
    height: 100%;
    width: 80%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    background: transparent;
}
.title-container {
    height: 45px;
    line-height: 45px;
    width: 100%;
    box-sizing: border-box;
    padding: 0 20px;
    font-size: 14px;
    text-align: left;
    background: transparent;
}
.info-container {
    height: 480px;
    width: 100%;
    overflow: auto;
}
.info-item {
    height: auto;
    width: 100%;
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    margin: 20px 0;
}
.info-item.mine {
    flex-direction: row-reverse;
}
.info-item .avatar {
    height: 25px;
    width: 25px;
    border-radius: 50%;
    margin-top: 25px;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 10px 0 20px;
}
.info-item.mine .avatar {
    margin: 0 20px 0 10px;
}
.info-item .text-container {
    width: 545px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
.info-item.mine .text-container {
    flex-direction: row-reverse;
}
.text-container .text {
    max-width: 360px;
    line-height: 20px;
    font-size: 12px;
    padding: 5px;
    border-radius: 5px;
    text-align: left;
    background: rgba(0, 0, 0, 0.4);
    color: white;
    word-break: break-all;
}
.input-container {
    height: 250px;
    width: 100%;
    box-sizing: border-box;
    border-top: 0px solid rgb(245, 245, 248);
    background: rgba(40, 40, 40, 0.1);
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
.input-container .tools-bar {
    height: 36px;
    width: 100%;
    box-sizing: border-box;
    padding:0 0px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.tools-icon {
    height: 20px;
    width: 20px;
    color: rgb(255, 255, 255);
    cursor: pointer;
    -webkit-transition-duration: 200ms;
    transition-duration: 200ms;
}
.tools-icon:hover {
    -webkit-transform: scale(1.2, 1.2) translate3d(0, 0, 0);
    transform: scale(1.2, 1.2) translate3d(0, 0, 0);
}
.tools-icon.disable {
    cursor: not-allowed;
}
.input-container textarea {
    height: 182px;
    width: 100%;
    border: none;
    outline: none;
    box-sizing: border-box;
    padding: 10px;
    resize: none;
    background: rgba(0, 0, 0, 0.4);
    color: white;
}
.input-container textarea:disabled {
    cursor: not-allowed;
    background: rgba(0, 0, 0, 0.2);
    color: white;
}

.submitButton {
    color: white;
    background: #4898ff;
    width: 30%;
    height: 36px;
    line-height: 36px;
}
.submitButton:hover {
    color: white;
    background: #7098ff;
}
::-webkit-scrollbar {
  width: 0;
}
</style>