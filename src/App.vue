<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <copy-right />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/array";
import CopyRight from "./components/CopyRight.vue";
import ResultScreen from "./components/ResultScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CopyRight,
  },

  data() {
    return {
      settings: {
        totalBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },

      statusMatch: "default",
      timer: 0,
    };
  },

  methods: {
    onHandleBeforeStart(config) {
      console.log("running handle before start, ", config);
      this.settings.totalBlocks = config.totalBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];

      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );

      this.settings.startedAt = new Date().getTime();

      // data ready
      this.statusMatch = "match";
    },
    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt;

      this.statusMatch = "result";
    },
  },
};
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
