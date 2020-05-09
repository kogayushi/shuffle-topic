<template>
  <div id="app">
    <div>
      <h2>あなたのお題</h2>
      <p>{{ currentTopic }}</p>
    </div>
    <div>
      <button :disabled="rouletteId" @click="start">スタート</button>
      <button @click="stop">ストップ</button>
    </div>
    <div>
      <h2>タイマー</h2>
      <p>残り{{ currentRemainingSecond }} 秒</p>
    </div>
    <div>
      <h2>お題</h2>
      <p>
        <input v-model="topics[1]" />
      </p>
      <p>
        <input v-model="topics[2]" />
      </p>
      <p>
        <input v-model="topics[3]" />
      </p>
      <p>
        <input v-model="topics[4]" />
      </p>
      <p>
        <input v-model="topics[5]" />
      </p>
      <p>
        <input v-model="topics[6]" />
      </p>
    </div>
    <div>
      <h2>タイマー設定（秒）</h2>
      <p>
        <input v-model="remainingSecond" />
      </p>
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
        6: "TBD"
      },
      rouletteId: null,
      timeId: null,
      remainingSecond: 360,
      currentRemainingSecond: 360
    };
  },
  methods: {
    start() {
      console.log("start");
      if (!this.rouletteId) {
        const id = setInterval(() => {
          const index = Math.floor(Math.random() * (max + 1 - min)) + min;
          this.currentTopic = this.topics[index];
        }, 200);
        this.rouletteId = id;
      }

      if (this.timeId) {
        clearInterval(this.timeId);
        this.timeId = null;
      }
    },
    stop() {
      console.log("stop");
      if (this.rouletteId) {
        clearInterval(this.rouletteId);
        this.rouletteId = null;
      }

      this.currentRemainingSecond = this.remainingSecond;
      if (this.timeId) {
        clearInterval(this.timeId);
      }
      const id = setInterval(() => {
        if (this.currentRemainingSecond > 0) {
          this.currentRemainingSecond -= 1;
        } else {
          clearInterval(this.timeId);
        }
      }, 1000);
      this.timeId = id;
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
</style>
