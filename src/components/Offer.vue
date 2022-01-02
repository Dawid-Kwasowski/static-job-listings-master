<template>
  <div class="offer">
    <div class="offer__container">
      <div class="offer__content">
        <div class="offer__company-logo">
          <img :src="require(`../assets/images/${offer.logo}`)" alt="company logo" />
        </div>
        <header class="offer__header">
          <h5 class="offer__company-name">{{ offer.company }}</h5>
          <div class="pills">
            <div v-if="offer.new" class="pills__pill">New!</div>
            <div v-if="offer.featured" class="pills__pill pills__pill--bg-dark">
              Featured
            </div>
          </div>
        </header>
        <div class="offer__info">
          <h3 class="offer__position">{{ offer.position }}</h3>
          <ul class="offer__info-list">
            <li class="offer__info-item">{{ offer.postedAt }}</li>
            <li class="offer__info-item">{{ offer.contract }}</li>
            <li class="offer__info-item">{{ offer.location }}</li>
          </ul>
        </div>
      </div>
      <div class="offer__horizontal-line"></div>
      <div class="offer__tags">
        <Tabs
          v-for="(item, index) in filters"
          :key="index"
          :content="item"
          @click="addToFilters(item)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Tabs from "@/components/Tabs.vue";
export default {
  components: {
    Tabs,
  },
  props: {
    offer: Object,
  },
  computed: {
    filters() {
      const { languages, role, level, tools } = this.offer;
      return [role, level, languages, tools].flat();
    },
  },
  methods: {
    addToFilters(payload) {
      return this.$emit("addToList", payload);
    },
  },
};
</script>

<style lang="scss">
// pallete of colors
$primary-color: hsl(180, 29%, 50%);
$secondary-color: hsl(180, 8%, 52%);
$dark-grayish-cyan-color: hsl(180, 14%, 20%);

.offer {
  max-width: 100%;
  min-height: 250px;
  margin: 25px 0;
  border-radius: 5px;
  border-left: 5px solid $primary-color;
  -webkit-box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  -moz-box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  box-shadow: 0px 33px 56px -30px rgba(88, 167, 167, 1);
  &__header {
    margin: 5px 0;
    display: flex;
    align-items: center;
  }
  &__container {
    padding: 0 20px;
  }
  &__content {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  &__company-logo {
    width: 50px;
    &--offset {
      transform: translateY(-45%);
    }
    @media (min-width: 375px) {
      width: 80px;
    }
    img {
      width: 100%;
    }
  }
  &__company-name {
    color: $primary-color;
    font-size: 18px;
    font-weight: 700;
  }
  &__position {
    color: $dark-grayish-cyan-color;
    font-size: 18px;
    font-weight: 700;
  }
  &__info {
    margin: 10px 0;
  }
  &__info-list {
    display: flex;
    margin: 10px 0;
  }

  &__info-item {
    margin: 5px 20px 0 0;
    color: $secondary-color;
    font-weight: 500;
    font-size: 16px;
    &:first-child {
      list-style: none;
    }
  }
  &__horizontal-line {
    height: 1px;
    width: 100%;
    background: $dark-grayish-cyan-color;
  }
  &__tags {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    padding: 15px 0;
  }
}
.pills {
  display: flex;
  margin: 0 5px;
  &__pill {
    font-weight: 700;
    font-size: 18px;
    text-transform: uppercase;
    letter-spacing: 1.3px;
    background: $primary-color;
    color: white;
    margin: 5px;
    padding: 6px 12px;
    border-radius: 20px;
    &--bg-dark {
      background: $dark-grayish-cyan-color;
    }
  }
}
</style>
