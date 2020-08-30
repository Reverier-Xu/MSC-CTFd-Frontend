<template>
    <div class="top-container">
        <!-- 关闭最大化最小化 按钮 -->
        <div class="button-container">
            <div class="red" @click="jump('index')"></div>
        </div>
        <!-- 中间导航按钮 -->
        <div class="nav-contaier">
            <font-awesome-icon
                icon="comment-dots"
                :class="[page == 'Challenges' ? 'active' : '' ,'nav-icon']"
                @click="jump('challenges')"
            />
        </div>
        <!-- 右边头像 -->
        <div class="avatar-container">
            <div
                class="avatar"
                @click="logOut"
                @mouseover="logout = true"
                @mouseout="logout = false"
            >
                <img src="../../static/images/xdmsc.png" title="登出" v-show="!logout" />
                <div class="logout" v-show="logout">
                    <font-awesome-icon icon="sign-out-alt" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { library } from "@fortawesome/fontawesome-svg-core";
import {
    faCommentDots,
    faThLarge,
    faUser,
    faSignOutAlt
} from "@fortawesome/free-solid-svg-icons";
import ajax from '../tools/ajax'

library.add(faCommentDots);
library.add(faThLarge);
library.add(faUser);
library.add(faSignOutAlt);

export default {
    name: "headbar",
    data() {
        return {
            page: "",
            logout: false
        };
    },
    computed: {},
    methods: {
        jump(url) {
            if (url === "team") {
                this.$router.push("/team/me");
            } else {
                this.$router.push("/" + url);
            }
        },
        logOut() {
            ajax.get("/logout")
                .then(resp => {
                    if (resp.success === true) {
                        localStorage.removeItem("team_id");
                        this.$router.push("/login");
                    }
                })
                .catch(error => console.log(error));
        }
    },
    created() {
        this.page = this.$route.name;
    },
    beforeUpdate() {
        this.page = this.$route.name;
    },
    mounted() {}
};
</script>

<style scoped>
.top-container {
    height: 55px;
    width: 100%;
    background: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.button-container {
    height: 100%;
    width: 75px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.button-container > div {
    height: 12px;
    width: 12px;
    border-radius: 50%;
    margin: 0 4px;
    cursor: pointer;
}
.button-container .red {
    background: rgb(252, 71, 72);
}
.button-container .yellow {
    background: none;
}
.button-container .green {
    background: none;
}

.avatar-container {
    margin: 0 10px;
}
.avatar {
    height: 30px;
    width: 30px;
    border-radius: 50%;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}
.avatar > img {
    height: 100%;
    width: 100%;
}

.nav-icon {
    height: 28px;
    width: 24px;
    color: rgb(241, 241, 241);
    margin: 0 20px;
    cursor: pointer;
}
.nav-icon.active {
    color: rgb(28, 167, 242);
}
.logout {
    height: 100%;
    width: 100%;
    background: rgb(244, 244, 244);
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>