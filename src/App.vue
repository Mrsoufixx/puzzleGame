<script setup>
import "./style.css";
</script>

<template>
  <div class="flex flex-row justify-center items-center gap-5 mt-10">
    <img
      @click="clickToFlip(index)"
      v-for="(item, index) in items"
      :src="item.isFlip ? item.iconSrc : cached"
      class="w-44 h-44 border border-black rounded-xl"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      cached:
        "https://c8.alamy.com/comp/2ACPGGT/bunch-of-cards-flipped-2ACPGGT.jpg",
      items: [
        {
          mark: "first",

          iconSrc:
            "https://media.istockphoto.com/id/1154859274/vector/signs-playing-cards-casino-isolated-signs-red-black-color-poker-signs.jpg?s=612x612&w=0&k=20&c=JJdoqUMNkiwmjR1pTi_c2g7OwYL255ux2EmdCjIlHRA=",
          isFlip: false,
        },
        {
          mark: "second",
          iconSrc:
            "https://images.unsplash.com/photo-1541963463532-d68292c34b19?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8Mnx8fGVufDB8fHx8&w=1000&q=80",
          isFlip: false,
        },
        {
          mark: "first",
          iconSrc:
            "https://media.istockphoto.com/id/1154859274/vector/signs-playing-cards-casino-isolated-signs-red-black-color-poker-signs.jpg?s=612x612&w=0&k=20&c=JJdoqUMNkiwmjR1pTi_c2g7OwYL255ux2EmdCjIlHRA=",
          isFlip: false,
        },
        {
          mark: "second",
          iconSrc:
            "https://images.unsplash.com/photo-1541963463532-d68292c34b19?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8Mnx8fGVufDB8fHx8&w=1000&q=80",
          isFlip: false,
        },
      ],
    };
  },
  methods: {
    clickToFlip(index) {
      if (!this.items[index].isFlip) {
        this.items[index].isFlip = true;
        let currentSrc = this.items[index].iconSrc;
        for (let i = 0; i < this.items.length; i++) {
          if (i !== index && this.items[i].isFlip) {
            if (currentSrc === this.items[i].iconSrc) {
              alert("matched");
            } else {
              this.items[i].isFlip = false;
            }
          }
        }
      }
    },
  },
};
</script>
