<template>
  <div
    :class="white ? 'cardLight' : 'card'"
    class="grid grid-cols-4 text-gray-200 gap-3  p-10 dark:text-gray-500"
  >
    <div
      class="col-span-4 dark:text-gray-600 text-right font-bold py-2 text-4xl shadow rounded mb-2 display"
    >
      <span class="mx-2 ">{{ current || 0 }}</span>
    </div>
    <div
      @click="clear"
      class="grid justify-center content-center text-3xl  text-yellow-500   "
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>AC</span>
    </div>
    <div
      @click="sign"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span> <PlusMinusVariant :size="30"/></span>
    </div>
    <div
      @click="percent"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span> <PercentOutline :size="30" /> </span>
    </div>
    <div
      @click="divide"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span> <SlashForward :size="30"/></span>
    </div>
    <div
      @click="append('7')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>7</span>
    </div>
    <div
      @click="append('8')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>8</span>
    </div>
    <div
      @click="append('9')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>9</span>
    </div>
    <div
      @click="times"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span><CloseThick :size="30"/></span>
    </div>
    <div
      @click="append('4')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>4</span>
    </div>
    <div
      @click="append('5')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>5</span>
    </div>
    <div
      @click="append('6')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>6</span>
    </div>
    <div
      @click="minus"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>-</span>
    </div>
    <div
      @click="append('1')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>1</span>
    </div>
    <div
      @click="append('2')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>2</span>
    </div>
    <div
      @click="append('3')"
      class="grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>3</span>
    </div>
    <div
      @click="plus"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>+</span>
    </div>
    <div
      @click="append('0')"
      class="col-span-2 grid justify-center content-center text-3xl"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>0</span>
    </div>
    <div
      @click="dot"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>.</span>
    </div>
    <div
      @click="equal"
      class="grid justify-center content-center text-3xl text-yellow-500"
      :class="white ? 'neuWhite' : 'neu'"
    >
      <span>=</span>
    </div>
  </div>
</template>

<script>
// import MenuIcon from "vue-material-design-icons/Menu.vue";
import PlusMinusVariant from "vue-material-design-icons/PlusMinusVariant.vue";
import PercentOutline from "vue-material-design-icons/Percent.vue";
import SlashForward from "vue-material-design-icons/SlashForward.vue";
import CloseThick from "vue-material-design-icons/Close.vue";
import gsap from "gsap";
export default {
  components: { PlusMinusVariant, PercentOutline, SlashForward, CloseThick },
  props: ["mode"],
  data() {
    return {
      colorMode: this.mode,
      white: false,
      previous: null,
      current: "",
      operatorClicked: false,
      operator: null,
    };
  },
  mounted() {
    console.log(this.colorMode);
  },
  methods: {
    newMode() {
      if (this.mode) {
        this.white = true;
      } else {
        this.white = false;
      }
    },
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    divide() {
      this.operator = (a, b) => (a / b) * 100;
      this.previous = this.current;

      this.operatorClicked = true;
    },
    times() {
      this.operator = (a, b) => a * b;
      this.previous = this.current;

      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previous = this.current;

      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.previous = this.current;

      this.operatorClicked = true;
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
  },
  watch: {
    mode: function() {
      this.newMode();
    },
  },
  mounted() {
    // gsap.from(this.$refs.btn, { opacity: 0.5, duration: 0.5, y: 30 });
    gsap.from(".neu", {
      opacity: 0,
      duration: 0.5,
      y: 50,
      delay: 1,
      stagger: {
        each: 0.1,
        from: "start",

        ease: "power2.in",
      },
    });
    gsap.from(".display", {
      opacity: 0,
      duration: 0.5,
      y: -100,
      delay: 0.3,
    });
    gsap.from(".card", {
      opacity: 0,
      duration: 1,
      delay: 0.3,
      ease: "power1.in",
    });
  },
};
</script>

<style lang="scss">
.card {
  border-radius: 11px;
  background: #262626;
  box-shadow: 20px 20px 50px #1f1f1f, -20px -20px 50px #2d2d2d;
}
.cardLight {
  border-radius: 11px;
  background: #e5e7eb;
  box-shadow: 19px 19px 38px #d5d7db, -19px -19px 38px #f5f7fb;
}
.neu {
  cursor: pointer;
  padding: 0.6rem;
  margin: 0rem;
  border-radius: 15px;
  background: linear-gradient(145deg, #292929, #222222);
  box-shadow: 5px 5px 10px #1d1d1d, -5px -5px 10px #2f2f2f;
  &:hover {
    border-radius: 15px;
    background: #262626;
    box-shadow: 5px 5px 10px #1f1f1f, -5px -5px 10px #2d2d2d;
  }
  &:active {
    border-radius: 15px;
    background: linear-gradient(145deg, #222222, #292929);
    box-shadow: 5px 5px 10px #1f1f1f, -5px -5px 10px #2d2d2d;
  }
}
.neuWhite {
  cursor: pointer;
  padding: 0.6rem;
  margin: 0rem;
  border-radius: 15px;
  background: linear-gradient(145deg, #f5f7fb, #ced0d4);
  box-shadow: 5px 5px 10px #ced0d4, -5px -5px 10px #fcfeff;
  &:hover {
    border-radius: 15px;
    background: #e5e7eb;
    box-shadow: 5px 5px 10px #ced0d4, -5px -5px 10px #fcfeff;
  }
  &:active {
    border-radius: 15px;
    background: linear-gradient(145deg, #ced0d4, #f5f7fb);
    box-shadow: 5px 5px 10px #ced0d4, -5px -5px 10px #fcfeff;
  }
}
</style>
