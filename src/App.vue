<template>
  <div id="app">
    <button
      @click="download"
      style="
        height: 40px;
        background-color: black;
        color: white;
        border-radius: 7px;
      "
    >
      Download
    </button>

    <!-- add ref attribute to the container which has to be downloaded -->
    <div ref="content">
      <img alt="Vue logo" src="./assets/logo.png" />
      <HelloWorld msg="Welcome to Your Vue.js App" />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { jsPDF } from "jspdf";
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  methods: {
    download() {
      // "l"= screen orientation 
      // "px" = unit
      // "a4" = pdf format
      const pdf = new jsPDF("l","px","a4");
      const html = this.$refs.content.innerHTML;
      pdf.html(html, {
        callback: (pdf) => {
          pdf.save("Invoice.pdf");
        },
        x: 45,
        y: 15,
        width: 400, 
        height:1240,
        windowWidth: 800
      });
    },
  },
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
