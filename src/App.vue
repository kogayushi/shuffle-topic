<template>
  <div id="app">
    <div>
      <h2>お題</h2>
      <transition name="fade">
        <p>{{ currentTopic }}</p>
      </transition>
    </div>
    <div>
      <button @click="start">スタート</button>
      <button @click="stop">ストップ</button>
    </div>
  </div>
</template>

<script>
var min = 1;
var max = 6;

export default {
  name: "App",
  data: function() {
    return {
      currentTopic: "ルーレットを回してね",
      topics: {
        1: "〇〇だった話",
        2: "人生を変えた●●",
        3: "グロービスに入社して〇〇だったこと",
        4: "受講あるある",
        5: "好きな芸能人",
        6: "尊敬する上司"
      },
      intervalId: null
    };
  },
  methods: {
    start() {
      console.log("start");
      if (!this.intervalId) {
        const id = setInterval(() => {
          const index = Math.floor(Math.random() * (max + 1 - min)) + min;
          this.currentTopic = this.topics[index];
        }, 200);
        this.intervalId = id;
      }
    },
    stop() {
      console.log("stop");
      if (this.intervalId) {
        clearInterval(this.intervalId);
        this.intervalId = null;
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.fade-enter-active,
.fade-leave-active {
  will-change: opacity;
  transition: opacity 225ms cubic-bezier(0.4, 0, 0.2, 1) 0ms;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
