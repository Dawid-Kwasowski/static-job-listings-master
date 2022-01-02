<template>
  <div class="tab">
    <div class="tab__container">
      <span class="tab__content">{{ content }}</span>
      <template v-if="isEditable">
        <div class="tab__remove-btn">
          <img src="@/assets/images/icon-remove.svg" alt="times" />
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isEditable: {
      default: false,
      type: Boolean,
    },
    content: {
      default: "Simple text",
      type: String,
    },
  },
};
</script>

<style lang="scss">
.tab {
  $ligt-grayish-cyan-color: hsl(180, 83%, 93%);
  $primary-color: hsl(180, 29%, 50%);
  background: $ligt-grayish-cyan-color;
  max-width: 200px;
  height: 30px;
  margin: 5px;
  cursor: pointer;
  border-radius: 5px;
  transition: transform 0.3s;
  &:hover {
    transform: scale(1.1);
  }
  &__container {
    display: flex;
    align-items: center;
    height: 100%;
    justify-content: space-between;
  }
  &__content {
    padding: 0 10px;
    font-weight: 700;
    font-size: 16px;
    color: $primary-color;
  }
  &__remove-btn {
    border-radius: 0 5px 5px 0;
    cursor: pointer;
    height: 30px;
    padding: 0 5px;
    display: flex;
    align-items: center;
    background: hsl(180, 29%, 50%);
  }
}
</style>
