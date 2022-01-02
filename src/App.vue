<template>
  <div class="container">
    <div class="container__banner">
      <!-- image -->
    </div>
    <main class="container__main-content">
      <!-- filtered area -->
      <section class="tabs-container">
        <!-- here will be placed a chips components  -->
        <div class="tabs-container__tabs-area">
          <Tabs
            v-for="(item, index) in filteredItems"
            :key="index"
            :content="item"
            :isEditable="true"
            @click="filteredItems.splice(index, 1)"
          />
        </div>
        <div class="tabs-container__clear">
          <button @click="filteredItems = []" class="btn">Clear</button>
        </div>
      </section>
      <section class="offers-container">
        <!-- here will be placed a job offers -->
        <transition-group name="fade">
          <article
            v-for="(offer, index) in offers"
            :key="index"
            v-show="showFilteredOffers(offer)"
          >
            <Offer :offer="offer" @addToList="addToFilters" />
          </article>
        </transition-group>
      </section>
    </main>
  </div>
</template>

<script>
import Offer from "./components/Offer.vue";
import Tabs from "./components/Tabs.vue";
export default {
  name: "App",
  components: {
    Offer,
    Tabs,
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
  methods: {
    addToFilters(payload) {
      if (this.filteredItems.some((el) => el == payload)) {
        return;
      } else {
        return this.filteredItems.push(payload);
      }
    },
    showFilteredOffers(offer) {
      const { role, level, languages, tools } = offer;
      const flattedArr = [role, level, languages, tools].flat();
      if (this.filteredItems.length === 0) {
        return true;
      } else {
        return flattedArr.includes(this.filteredItems[this.filteredItems.length - 1]);
      }
    },
  },
};
</script>

<style lang="scss">
// colors
$background-color: hsl(180, 52%, 96%);
$primary-color: hsl(180, 29%, 50%);
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
.tabs-container {
  -webkit-box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  -moz-box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  min-height: 100px;
  width: 100%;
  display: flex;
  background: $background-color;
  padding: 10px;
  &__tabs-area {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
  }
  &__clear {
    min-height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
.btn {
  border: none;
  outline: none;
  padding: 10px;
  color: $primary-color;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  border-radius: 5px;
  background: transparent;
  transition: background 0.3s, color 0.3s;
  &:hover,
  &:focus {
    background: $primary-color;
    color: white;
  }
}

// animations
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(50px);
}
</style>
