<template>
  <nav
    class="flex items-center justify-between px-6 bg-gray-800 dark:bg-gray-200 text-gray-100 dark:text-gray-900 h-16 shadow "
  >
    <h2 class=" uppercase text-lg tracking-widest">Calculator</h2>

    <!-- Toggle Button -->
    <label for="toogleA" class="flex items-center cursor-pointer">
      <!-- toggle -->
      <div class="relative">
        <!-- input -->
        <input
          id="toogleA"
          type="checkbox"
          class="hidden"
          @click="$emit('update:mode', (newMode = !newMode))"
        />
        <!-- line -->
        <div
          class="w-10 h-4 bg-gray-600 dark:bg-gray-400 rounded-full shadow-inner"
        ></div>
        <!-- dot -->
        <div
          class="toggle__dot absolute w-6 h-6 bg-gray-500 rounded-full shadow  left-0"
        ></div>
      </div>
      <!-- label -->
      <div class="ml-3 text-gray-500 font-medium dark:text-yellow-600">
        Light Mode
      </div>
    </label>
  </nav>
</template>
<script>
export default {
  props: ["mode"],
  name: "Navbar",
  data() {
    return {
      newMode: this.mode,
    };
  },
  methods: {
    // changeMode() {
    //   this.newMode = !this.newMode;
    // },
  },
};
</script>

<style>
.toggle__dot {
  top: -0.25rem;
  left: -0.3rem;
  transition: all 0.3s ease-in-out;
}

input:checked ~ .toggle__dot {
  transform: translateX(100%);
  background-color: #f3a600;
}
</style>
