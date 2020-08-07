<template>
  <div id="app">
    <h1>Given</h1>
    <br />
    <hr />
    <!-- PROBLEM 2: Color the text in each button that goes with the corresponding status from the payload-->
    <prompt
      v-for="{ id, status, color } in list"
      :key="id"
      @change="update"
      :id="id"
      :status="status"
      class="item"
      :style="{ color }"
    ></prompt>
    <!-- PROBLEM 3: Show latest status text that was clicked most recently om the color which goes with the status -->
    <LastStatus :currentStatus="currentStatus" />
  </div>
</template>

<script>
import prompt from "./components/prompt.vue";
import LastStatus from "./components/LastStatus.vue";
window.random = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;

const MOCK_BACKEND = {
  getList() {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve([
          { id: 0, status: "success", color: "green" },
          { id: 1, status: "pending", color: "orange" },
          { id: 2, status: "failed", color: "red" },
          { id: window.random(3, 10), status: "new", color: "blue" },
        ]);
      }, 500);
    });
  },
};

export default {
  name: "App",
  components: { prompt, LastStatus },
  async beforeMount() {
    this.list = await MOCK_BACKEND.getList();
  },
  data() {
    return {
      // PROBLEM 1: Instead static data integrate async payload that will come from MOCK_BACKEND when vue the vue app mounts (see towards the end the this file)
      list: [],
      currentStatus: "",
    };
  },
  methods: {
    update(status) {
      // instead of logging it, show it on the view which status was updated most recently
      // console.log("update status: " + status);
      this.currentStatus = status;
    },
  },
};
</script>

<style>
#app {
  padding: 10px;
}
.item {
  margin: 0 10px 0 0;
}
</style>
