<template>
  <div class="container">
    <div class="container__banner">
      <!-- image -->
    </div>
    <main class="container__main-content">
      <!-- filtered area -->
      <section class="chips-container">
        <!-- here will be placed a chips components  -->
      </section>
      <section class="offers-container">
        <!-- here will be placed a job offers -->
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  // single source of truth
  data() {
    return {
      offers: []
    }
  }
}
</script>

<style lang="scss">
</style>
