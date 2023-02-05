<script setup>
import "./style.css";
</script>

<template>
  <div class="flex flex-row justify-center items-center gap-5 mt-10 relative">
    <div
      v-for="item in memoryCards"
      class="w-44 h-44 rounded-xl flip-container relative"
      :class="{ flipped: item.isFlip, matched: item.isMatch }"
      @click="flipCard(item)"
    >
      <div class="w-44 h-44 front border rounded shadow">
        <img
          class="rounded w-44 h-44"
          src="https://c8.alamy.com/comp/2ACPGGT/bunch-of-cards-flipped-2ACPGGT.jpg"
        />
      </div>
      <div class="back rounded border">
        <img :src="item.iconSrc" class="w-44 h-44 rounded" />
      </div>
    </div>
    <div class="flex justify-center py-3">
      <div class="turns p-3">
        <span class="btn btn-info"
          >Turns :
          <span
            class="badge"
            :class="finish ? 'badge-success' : 'badge-light'"
            >{{ turns }}</span
          >
        </span>
      </div>
      <div class="totalTime p-3">
        <span class="btn btn-info"
          >Total Time :
          <span class="badge" :class="finish ? 'badge-success' : 'badge-light'"
            >{{ min }} : {{ sec }}</span
          ></span
        >
      </div>
      <div class="totalTime p-3">
        <button class="btn btn-info" @click="reset" :disabled="!start">
          Restart
        </button>
      </div>
    </div>
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
          name: "first",

          iconSrc:
            "https://media.istockphoto.com/id/1154859274/vector/signs-playing-cards-casino-isolated-signs-red-black-color-poker-signs.jpg?s=612x612&w=0&k=20&c=JJdoqUMNkiwmjR1pTi_c2g7OwYL255ux2EmdCjIlHRA=",
        },
        {
          name: "second",
          iconSrc:
            "https://images.unsplash.com/photo-1541963463532-d68292c34b19?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8Mnx8fGVufDB8fHx8&w=1000&q=80",
        },
      ],
      memoryCards: [],
      flippedCards: [],
      finish: false,
      start: false,
      turns: 0,
      totalTime: {
        minutes: 0,
        seconds: 0,
      },
    };
  },

  created() {
    this.reset();
    this.items.forEach((card) => {
      card["isFlip"] = false;
      card["isMatch"] = false;
    });

    this.memoryCards = _.shuffle(
      this.memoryCards.concat(_.cloneDeep(this.items), _.cloneDeep(this.items))
    );
  },

  methods: {
    flipCard(card) {
      if (card.isMatch || card.isFlip || this.flippedCards.length === 2) return;
      if (!this.start) {
        this._startGame();
      }
      card.isFlip = true;
      if (this.flippedCards.length < 2) this.flippedCards.push(card);
      if (this.flippedCards.length === 2) this._match(card);
    },
    _match(card) {
      this.turns++;
      if (this.flippedCards[0].name === this.flippedCards[1].name) {
        setTimeout(() => {
          this.flippedCards.forEach((card) => (card.isMatch = true));
          this.flippedCards = [];
          if (this.memoryCards.every((card) => card.isMatch === true)) {
            clearInterval(this.interval);
            this.finish = true;
          }
        }, 400);
      } else {
        setTimeout(() => {
          this.flippedCards.forEach((card) => {
            card.isFlip = false;
          });
          this.flippedCards = [];
        }, 800);
      }
    },
    _startGame() {
      this._tick();
      this.interval = setInterval(this._tick, 1000);
      this.start = true;
    },

    _tick() {
      if (this.totalTime.seconds !== 59) {
        this.totalTime.seconds++;
        return;
      }
      this.totalTime.minutes++;
      this.totalTime.seconds = 0;
    },
    reset() {
      clearInterval(this.interval);

      this.items.forEach((card) => {
        card["isFlip"] = false;
        card["isMatch"] = false;
      });

      setTimeout(() => {
        this.memoryCards = [];
        this.memoryCards = _.shuffle(
          this.memoryCards.concat(
            _.cloneDeep(this.items),
            _.cloneDeep(this.items)
          )
        );
        this.totalTime.minutes = 0;
        this.totalTime.seconds = 0;
        this.start = false;
        this.finish = false;
        this.turns = 0;
        this.flippedCards = [];
      }, 600);
    },
  },
  computed: {
    sec() {
      if (this.totalTime.seconds < 10) {
        return "0" + this.totalTime.seconds;
      }
      return this.totalTime.seconds;
    },
    min() {
      if (this.totalTime.minutes < 10) {
        return "0" + this.totalTime.minutes;
      }
      return this.totalTime.minutes;
    },
  },
};
</script>
