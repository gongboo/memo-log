<template>
  <div class="hello">
    <div class="log-board">
      <textarea v-model="txt" class="log-textarea"></textarea>
    </div>

    <select v-model="selectedOp" name="options">
      <option value="ACT" selected>ACT</option>
      <option value="ERR">ERR</option>
      <option value="INFO">INFO</option>
    </select>
    <input v-model="inputTxt" type="text" @keyup.enter.prevent="handleSubmit" />
    <button @click="handleSubmit">enter</button>
  </div>
</template>

<script>
import { defineComponent } from "vue";
// import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

export default defineComponent({
  name: "HomeView",
  props: {
    msg: String,
  },
  data() {
    return {
      count: 0,
      txt: "texts",
      inputTxt: "",
      selectedOp: "ACT",
      currentTime: "",
    };
  },
  methods: {
    getTime() {
      const now = new Date();
      const hours = String(now.getHours()).padStart(2, "0");
      const minutes = String(now.getMinutes()).padStart(2, "0");
      const seconds = String(now.getSeconds()).padStart(2, "0");

      this.currentTime = `${hours}:${minutes}:${seconds}`;
      return this.currentTime;
    },
    // handleChange() { },
    handleSubmit(event) {
      if (event) event.preventDefault(); // 이벤트 기본 동작 방지

      this.txt +=
        "\n[" + this.getTime() + "]" + this.selectedOp + "-" + this.inputTxt;
      this.inputTxt = "";
    },
  },
  // components: {
  //   HelloWorld,
  // },
});
</script>

<style scoped>
.log-textarea {
  width: 300px;
  height: 200px;
  resize: none;
  overflow-y: auto;
  padding: 10px;
  font-family: monospace;
}

.pre-wrap {
  white-space: pre-wrap;
}
</style>
