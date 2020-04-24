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
                <nav class="menu">
                    <input type="checkbox" href="#" class="menu-open" name="menu-open" id="menu-open" />
                    <label class="menu-open-button" for="menu-open">
                        <span class="lines line-1"></span>
                        <span class="lines line-2"></span>
                        <span class="lines line-3"></span>
                    </label>

                    <a href="#" class="menu-item blue">
                        <font-awesome-icon
                                :icon="['fab', 'docker']"
                                width="1em"
                                fixed-width
                                @click="send('获取环境')"
                        />
                    </a>
                    <a href="#" class="menu-item green">
                        <font-awesome-icon
                                :icon="['fas', 'user-clock']"
                                width="1em"
                                fixed-width
                                @click="send('延长时限')"
                        />
                    </a>
                    <a href="#" class="menu-item red">
                        <font-awesome-icon
                            :icon="['fas', 'stop-circle']"
                            width="1em"
                            fixed-width
                            @click="send('销毁环境')"
                    />
                    </a>
                </nav>
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
};
</script>

<style>
    .menu-item,
    .menu-open-button {
        background: #EEEEEE;
        border-radius: 100%;
        width: 30px;
        height: 30px;
        margin-left: -15px;
        position: absolute;
        color: #FFFFFF;
        text-align: center;
        line-height: 30px;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
        -webkit-transition: -webkit-transform ease-out 200ms;
        transition: transform ease-out 200ms, -webkit-transform ease-out 200ms;
    }

    .menu-open {
        display: none;
    }

    .lines {
        width: 10px;
        height: 2px;
        background: #596778;
        display: block;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-left: -5px;
        margin-top: -1px;
        -webkit-transition: -webkit-transform 200ms;
        transition: -webkit-transform 200ms;
        transition: transform 200ms, -webkit-transform 200ms;
    }

    .line-1 {
        -webkit-transform: translate3d(0, -5px, 0);
        transform: translate3d(0, -5px, 0);
    }

    .line-2 {
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }

    .line-3 {
        -webkit-transform: translate3d(0, 5px, 0);
        transform: translate3d(0, 5px, 0);
    }

    .menu-open:checked + .menu-open-button .line-1 {
        -webkit-transform: translate3d(0, 0, 0) rotate(45deg);
        transform: translate3d(0, 0, 0) rotate(45deg);
    }

    .menu-open:checked + .menu-open-button .line-2 {
        -webkit-transform: translate3d(0, 0, 0) scale(0.1, 1);
        transform: translate3d(0, 0, 0) scale(0.1, 1);
    }

    .menu-open:checked + .menu-open-button .line-3 {
        -webkit-transform: translate3d(0, 0, 0) rotate(-45deg);
        transform: translate3d(0, 0, 0) rotate(-45deg);
    }

    .menu {
        position: relative;
        width: 30px;
        height: 30px;
        text-align: center;
        box-sizing: border-box;
        font-size: 26px;
    }

    .menu-item:hover {
        background: #EEEEEE;
        color: #3290B1;
    }

    .menu-item:nth-child(3) {
        -webkit-transition-duration: 180ms;
        transition-duration: 180ms;
    }

    .menu-item:nth-child(4) {
        -webkit-transition-duration: 180ms;
        transition-duration: 180ms;
    }

    .menu-item:nth-child(5) {
        -webkit-transition-duration: 180ms;
        transition-duration: 180ms;
    }


    .menu-open-button {
        z-index: 2;
        -webkit-transition-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
        transition-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
        -webkit-transition-duration: 400ms;
        transition-duration: 400ms;
        -webkit-transform: scale(1.1, 1.1) translate3d(0, 0, 0);
        transform: scale(1.1, 1.1) translate3d(0, 0, 0);
        cursor: pointer;
        box-shadow: 3px 3px 0 0 rgba(0, 0, 0, 0.14);
    }

    .menu-open-button:hover {
        -webkit-transform: scale(1.2, 1.2) translate3d(0, 0, 0);
        transform: scale(1.2, 1.2) translate3d(0, 0, 0);
    }

    .menu-open:checked + .menu-open-button {
        -webkit-transition-timing-function: linear;
        transition-timing-function: linear;
        -webkit-transition-duration: 200ms;
        transition-duration: 200ms;
        -webkit-transform: scale(0.8, 0.8) translate3d(0, 0, 0);
        transform: scale(0.8, 0.8) translate3d(0, 0, 0);
    }

    .menu-open:checked ~ .menu-item {
        -webkit-transition-timing-function: cubic-bezier(0.935, 0, 0.34, 1.33);
        transition-timing-function: cubic-bezier(0.935, 0, 0.34, 1.33);
    }

    .menu-open:checked ~ .menu-item:nth-child(3) {
        transition-duration: 180ms;
        -webkit-transition-duration: 180ms;
        -webkit-transform: translate3d(0.08361px, -40.99997px, 0);
        transform: translate3d(0.08361px, -40.99997px, 0);
    }

    .menu-open:checked ~ .menu-item:nth-child(4) {
        transition-duration: 280ms;
        -webkit-transition-duration: 280ms;
        -webkit-transform: translate3d(45.9466px, -22.47586px, 0);
        transform: translate3d(45.9466px, -22.47586px, 0);
    }

    .menu-open:checked ~ .menu-item:nth-child(5) {
        transition-duration: 380ms;
        -webkit-transition-duration: 380ms;
        -webkit-transform: translate3d(45.9466px, 25.47586px, 0);
        transform: translate3d(45.9466px, 25.47586px, 0);
    }

    .blue {
        background-color: #669AE1;
        box-shadow: 3px 3px 0 0 rgba(0, 0, 0, 0.14);
        text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.12);
    }

    .blue:hover {
        color: #669AE1;
        text-shadow: none;
    }

    .green {
        background-color: #70CC72;
        box-shadow: 3px 3px 0 0 rgba(0, 0, 0, 0.14);
        text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.12);
    }

    .green:hover {
        color: #70CC72;
        text-shadow: none;
    }

    .red {
        background-color: #FE4365;
        box-shadow: 3px 3px 0 0 rgba(0, 0, 0, 0.14);
        text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.12);
    }

    .red:hover {
        color: #FE4365;
        text-shadow: none;
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
