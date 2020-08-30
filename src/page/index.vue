<template>
  <div class="container">
    <div id="minil-logo">
      <img src="static/images/xdmsc.png" alt="minil-logo" width="500px" />
    </div>
    <div class="jump-button" @click="start">
      <div class="button-text">开始</div>
    </div>
  </div>
</template>

<script>
import jQuery from "jquery";
export default {
  components: {},
  data() {
    return {
      countDownTime: "尚未开始",
      html: "",
    };
  },
  methods: {
    jump(url) {
      window.open(url);
    },
    start() {
      this.$router.push("/login");
    },
  },
  mounted() {
    (function ($) {})(jQuery);
  },
};
</script>

<style scoped>
* {
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
#minil-logo {
  position: absolute;
  z-index: 999;
  left: 50%;
  transform: translate(-50%, 0);
}
.container {
  background: transparent;
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
}
.jump-button {
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
  font-family: "Microsoft YaHei UI Light", sans-serif;
  font-size: 25px;
}
.button-text {
  padding-top: 20px;
  letter-spacing: 2px;
}
.jump-button:hover {
  background: cornflowerblue;
  border: solid #397cf5 1.5px;
  transform: translate(-50%, -5px);
  color: black;
}
</style>
