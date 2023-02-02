<script setup>
import "./style.css";
</script>

<template>
  <!-- <div class="flex justify-center items-center gap-5 mt-10">
    <span class="w-44 h-44 border border-black rounded"></span
    ><span class="w-44 h-44 border border-black rounded"></span
    ><span class="w-44 h-44 border border-black rounded"></span
    ><span class="w-44 h-44 border border-black rounded"></span>
  </div> -->

  <div class="flex justify-center items-center mt-4 mx-auto">
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      <div
        v-for="item in items"
        @click="clickToFlip"
        :class="(item.isFlip = !item.isFlip)"
        class="card w-44 h-44 m-2 cursor-pointer border border-gray-400 rounded-lg"
      ></div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      classFlip:
        "shadow-md border-opacity-0 transform -translate-y-1 transition-all duration-200",
      items: [
        {
          mark: "first",
          iconSrc: "",
          isFlip: false,
        },
        {
          mark: "second",
          iconSrc: "",
          isFlip: false,
        },
        {
          mark: "first",
          iconSrc: "",
          isFlip: false,
        },
        {
          mark: "second",
          iconSrc: "",
          isFlip: false,
        },
      ],
    };
  },
  methods: {
    clickToFlip() {
      {
        this.classFlip, (this.isFlip = true);
      }
    },
  },
};
</script>
