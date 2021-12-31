<template>
  <div class="container">
    <div class="container__banner">
      <!-- image -->
    </div>
    <main class="container__main-content">
      <!-- filtered area -->
      <section v-if="filteredItems.length > 0" class="tabs-container">
        <!-- here will be placed a chips components  -->
      </section>
      <section class="offers-container">
        <!-- here will be placed a job offers -->
        <article v-for="(offer, index) in offers" :key="index">
          <Offer :offer="offer" />
        </article>
      </section>
    </main>
  </div>
</template>

<script>
import Offer from "./components/Offer.vue";
export default {
  name: "App",
  components: {
    Offer,
  },
  // single source of truth
  data() {
    return {
      offers: [],
      filteredItems: [],
    };
  },
  // lifecycle methods
  beforeCreate() {
    // get data from db and initialize them before app component was created
    return fetch("http://192.168.1.24:8081/offers")
      .then((response) => response.json())
      .then((data) => {
        this.offers = data;
      });
  },
};
</script>

<style lang="scss">
// colors
$background-color: hsl(180, 52%, 96%);

* {
  @import url("https://fonts.googleapis.com/css2?family=Spartan:wght@500;700&display=swap");

  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

.container {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: flex-start;
  flex-basis: 100%;
  min-height: 100vh;
  background: $background-color;
  &__banner {
    min-height: 155px;
    width: 100%;
    background: no-repeat url("./assets/images/bg-header-mobile.svg");
    @media (min-width: 375px) {
      background: no-repeat url("./assets/images/bg-header-desktop.svg");
    }
  }
}
.offers-container {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: flex-start;
  margin: 10% 5%;
}
</style>
