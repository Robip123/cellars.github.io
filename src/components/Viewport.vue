<template>
  <div class="viewport">
    <img :src="image" class="image" />

    <div class="characters">
      <transition-group
        tag="div"
        enter-active-class="animated slideInLeft"
        leave-active-class="animated slideOutLeft flipped"
      >
        <img
          v-for="(src, index) in squad"
          :key="src"
          :src="src"
          :style="getCharacterStyle(index)"
          class="character"
        />
      </transition-group>

      <transition-group
        tag="div"
        enter-active-class="animated slideInRight"
        leave-active-class="animated slideOutRight"
      >
        <img
          v-for="(src, index) in encounters"
          :key="src"
          :src="src"
          :style="getCharacterStyle(index, true)"
          class="character"
        />
      </transition-group>
    </div>
  </div>
</template>

<script>
const offset = 7.5;

export default {
  computed: {
    image() {
      return this.$store.state.game.image;
    },
    squad() {
      return this.$store.state.game.squad;
    },
    encounters() {
      return this.$store.state.game.encounters;
    },
  },
  methods: {
    // DONT TOUCH THIS PLEASE
    // I FORGOT HOW THIS WORKS
    getCharacterStyle(index, encounter = false) {
      return {
        [encounter ? 'right' : 'left']: `${index * offset + offset / 4}vw`,
        zIndex: `${Math.floor(90 / (index + 1))}`,
      };
    },
  },
};
</script>

<style scoped>
.viewport {
  width: 65vw;
  position: relative;

  image-rendering: pixelated;
  image-rendering: crisp-edges;
}

@media (max-aspect-ratio: 11/7) {
  .viewport {
    width: auto;
  }
}

@media (min-aspect-ratio: 6/7) {
  .viewport {
    height: 100%;
  }
}

.image {
  width: 100%;
  height: 100%;
}

.characters {
  position: absolute;
  overflow: hidden;

  width: 100%;
  height: 100%;

  bottom: 0;
}

.character {
  position: absolute;

  width: auto;
  height: 70vh;

  bottom: 0;

  image-rendering: pixelated;
  image-rendering: crisp-edges;
}

@media (max-aspect-ratio: 11/7) {
  .character {
    height: auto;
    width: 20vw;
  }
}
</style>
