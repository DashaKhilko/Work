<template>
  <div>
    <button class="button" @click="currentComponent = 1">6 Этаж</button>
    <button class="button" @click="currentComponent = 2">7 Этаж</button>
    <button class="button" @click="currentComponent = 3">8 этаж</button>

    <component v-if="currentComponent === 1" is="SixthFloor" />
    <component v-if="currentComponent === 2" is="SeventhFloor" />
    <component v-if="currentComponent === 3" is="EighthFloor" />
  </div>
</template>

<script>
import EighthFloor from "./components/EighthFloor.vue";
import SeventhFloor from "./components/SeventhFloor.vue";
import SixthFloor from "./components/SixthFloor.vue";
import axios from "axios";

export default {
  components: {
    EighthFloor,
    SeventhFloor,
    SixthFloor,
  },

  data() {
    return {
      currentComponent: 1,
      items: [],
    };
  },
  async mounted() {
    try {
      const response = await axios.get(
        "https://bntp.by/wp-json/encore/bstp-tour/residents"
      );
      this.items = response.data;
      console.log(this.items[0].title);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
.button {
  background-color: #ddd;
  border: none;
  border-radius: 4px;
  color: #333;
  cursor: pointer;
  font-size: 16px;
  padding: 12px 16px;
  margin: 0 8px;
  text-align: center;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #bbb;
}
</style>
