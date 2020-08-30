<template>
    <div class="container">
        <div id="minil-logo">
            <img src="static/images/xdmsc.png" alt="minil-logo" width="500px">
        </div>
        <div class="jump-button" @click="start">
            <div class="button-text">开始</div>
        </div>
    </div>
</template>

<script>
import jQuery from 'jquery'
export default {
    components: {},
    data() {
        return {
            countDownTime: "尚未开始",
            html: ""
        };
    },
    methods: {
        jump(url) {
            window.open(url);
        },
        start() {
            this.$router.push("/login");
        }
    },
    mounted() {
        (function ($) {
        })(jQuery)
    }
};
</script>

<style scoped>
    *{
        user-select: none;
    }
    #bg {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 2;
    }

    #bg canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
    #minil-logo{
        position: absolute;
        z-index: 999;
        left: 50%;
        transform: translate(-50%,0);
    }
    #minil-title{
        z-index: 999;
        position: absolute;
        top: 55%;
        left: 50%;
        transform: translate(-50%,0);
    }
.container{
    background: linear-gradient(to bottom right, rgb(26,46,112), rgb(20,20,40));
    width: 100%;
    height: 100%;
    overflow: hidden;
    position: relative;
}
    ul{
        list-style: none;

    }
    .bubble{
        position: absolute;
        width: 100px;
        height: 100px;
        border-radius: 100%;
        background: #6495ed;
    }
    .bubble1{
        width: 600px;
        height: 600px;
        background: rgb(49, 89, 139);
        opacity: 0.5;
        left: 80%;
        top: -15%;
        animation: bubble1Ani 2s ease-in-out 1s infinite alternate;
    }
    @keyframes bubble1Ani{
        0%{
            top: -15%;
            background-color: #2fffac;
        }
        25%{
            top: -10%;
            background-color: #006680;
        }
        50%{
            top: -13%;
            background-color: #00e1ff;
        }
        75%{
            top: -17%;
            background-color: #007bff;
        }
        100%{
            top: -15%;
            background-color: #2fb6ff;
        }
    }
.bubble2{
    width: 300px;
    height: 300px;
    background: rgba(113, 87, 79, 0.8);
    left: 16%;
    top: 13%;
    animation: bubble2Ani 2s ease-in-out 1s infinite alternate;
}
    @keyframes bubble2Ani{
        0%{
            top: 11%;
            background-color: #7b817f;
        }
        25%{
            top: 14%;
            background-color: #815656;
        }
        50%{
            top: 10%;
            background-color: #ffa0d6;
        }
        75%{
            top: 13%;
            background-color: #b13ba6;
        }
        100%{
            top: 12%;
            background-color: #926f6f;
        }
    }
.bubble3{
    width: 400px;
    height: 400px;
    background: rgb(44, 29, 77);
    left: 60%;
    top: 40%;
    animation: bubble3Ani 2s ease-in-out 1s infinite alternate;
}
    @keyframes bubble3Ani{
        0%{
            top: 37%;
            background-color: #41264c;
        }
        25%{
            top: 41%;
            background-color: #b857ff;
        }
        50%{
            top: 38%;
            background-color: #ffa0d6;
        }
        75%{
            top: 39%;
            background-color: #b13ba6;
        }
        100%{
            top: 42%;
            background-color: #622769;
        }
    }
.bubble4{
    width: 500px;
    height: 500px;
    background: rgb(15, 52, 97);
    left: -5%;
    top: 70%;
    animation: bubble4Ani 2s ease-in-out 1s infinite alternate;
}
    @keyframes bubble4Ani{
        0%{
            top: 68%;
            background-color: #232d6b;
        }
        25%{
            top: 71%;
            background-color: #357ba7;
        }
        50%{
            top: 69%;
            background-color: #314486;
        }
        75%{
            top: 72%;
            background-color: #172270;
        }
        100%{
            top: 67%;
            background-color: #274c69;
        }
    }
.bubble5{
    width: 200px;
    height: 200px;
    background: rgb(100, 149, 237);
    left: 7%;
    animation: bubble5Ani 2s ease-in-out 1s infinite alternate;
}
    @keyframes bubble5Ani{
        0%{
            top: 1%;
            background-color: #5e72ee;
        }
        25%{
            top: -1%;
            background-color: #357ba7;
        }
        50%{
            top: 2%;
            background-color: #314486;
        }
        75%{
            top: 0%;
            background-color: #3b426e;
        }
        100%{
            top: 1%;
            background-color: #6dacde;
        }
    }
    .jump-button{
        position: absolute;
        z-index: 999;
        width: 300px;
        height: 80px;
        border: solid cornflowerblue 1.5px;
        border-radius: 40px;
        left: 50%;
        top: 55%;
        transform: translate(-50%, 0);
        margin-top: 150px;
        text-align: center;
        transition: all 0.2s ease-in-out;
        color: white;
        font-family: "Microsoft YaHei UI Light" ,sans-serif;
        font-size: 25px;
    }
    .button-text{
        padding-top: 20px;
        letter-spacing: 2px;
    }
    .jump-button:hover{
        background: cornflowerblue;
        border: solid #397cf5 1.5px;
        transform: translate(-50%, -5px);
        color: black;
    }
</style>
