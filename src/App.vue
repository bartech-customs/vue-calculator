<template>
  <div
    id="app"
    class="bg-gray-800 dark:bg-gray-200 h-full w-full min-h-screen  md:h-screen overflow-x-hidden md:overflow-y-hidden"
  >
    <Navbar :mode.sync="lightMode" />
    <div
      class="grid grid-cols-1 md:grid-cols-2  h-full justify-items-center  items-center"
    >
      <Side />
      <Calc
        :mode.sync="lightMode"
        class="row-start-1 md:col-start-2 mt-12 md:mt-0"
      />
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Side from "@/components/Side.vue";
import Calc from "@/components/Calc.vue";

export default {
  name: "App",
  components: {
    Navbar,
    Side,
    Calc,
  },
  data() {
    return {
      lightMode: false,
    };
  },
  methods: {
    newMode() {
      if (this.lightMode) {
        document.querySelector("html").classList.add("dark");
      } else {
        document.querySelector("html").classList.remove("dark");
      }
    },
  },
  watch: {
    lightMode: function() {
      this.newMode();
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Quicksand&display=swap");
#app {
  font-family: "Quicksand", sans-serif;
}
body {
  background-color: rgb(121, 121, 121);
}
</style>
