<script>
export default {
  props: {
    games: {
      type: Array,
      require: true,
    },
    currGame: {
      type: Object,
      require: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    setIdx(idx) {
      this.$emit("set-idx", idx);
    },
    goToDetails(id) {
      this.$router.push(`/games/${id}`);
    },
  },
};
</script>


<template>
  <section class="featured-games">
    <div class="game-display">
      <img :src="`${currGame.imgUrl}`" alt="Game Image" />
      <div class="darker-img"></div>
      <div class="game-info">
        <h1>{{ currGame.title }}</h1>
        <p>
          {{ currGame.description }}
        </p>
        <h4>Get for ${{ currGame.price }}</h4>
        <button @click="goToDetails(currGame._id)">Buy Now</button>
      </div>
    </div>
    <div class="featured-list">
      <div
        v-for="(game, idx) in games.slice(0, 5)"
        :key="idx"
        class="card"
        @click="setIdx(idx)"
      >
        <img :src="`${game.imgUrl}`" />
        <h4>{{ game.title }}</h4>
      </div>
    </div>
  </section>
</template>


<style lang="scss">
.featured-games {
  display: flex;
  flex-wrap: wrap;
}

.featured-list {
  display: flex;
  flex-direction: column;
  gap: 5px;
  grid-row: 1/-1;

  @media (max-width: 760px) {
    width: 100%;
  }
  .card {
    display: flex;
    padding: 10px;
    align-items: center;
    cursor: pointer;
    border-radius: 0.4em;
    transition: 0.3s;
    max-width: 250px;

    @media (max-width: 760px) {
      max-width: none;
    }

    &:hover {
      background-color: rgb(54, 54, 54);
    }

    img {
      height: 94px;
      width: 80px;
      object-fit: cover;
      border-radius: 0.3em;
    }
  }
}

.game-display {
  display: flex;
  flex: 2;
  position: relative;
  overflow: hidden;
  align-items: flex-end;
  border-radius: 0.5em;
  min-width: 350px;

  @media (max-width: 765px) {
    height: 500px;
    margin-bottom: 20px;
  }

  .game-info {
    padding: 15px;
    display: flex;
    flex-direction: column;
    color: white;
    gap: 20px;

    h1 {
      font-size: 38px;
      margin-block-end: 25px;
      font-family: monts-semibold;
    }

    p {
      max-width: 450px;
    }

    button {
      padding: 15px;
      transition: 0.3s;

      &:hover {
        color: var(--clr-white);
        background-color: var(--clr-highlight);
      }
    }
  }

  img {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    z-index: -2;
    object-fit: cover;
    object-position: center;
    filter: brightness(80%);
  }

  .darker-img {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
}
</style>