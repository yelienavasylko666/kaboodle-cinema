<template>
  <section>
    <div class="main">
      <img src="../assets/img/Rectangle7.png" class="main__img" />
      <img src="../assets/svg/Logocopy.png" class="main__logo" />
      <h1 class="main__text">
        Kabbodle
      </h1>
    </div>
  </section>
</template>

<script>
    export default {
        name: "Section1"
    }
</script>

<style  lang="scss">
.main {
  position: relative;
  overflow: hidden;

  &__img {
    width: 100%;
    height: 100%;
  }

  &__logo,
  &__text {
    position: absolute;
  }
  &__logo {
    left: 30%;
    top: 100px;
    height: 300px;

  }
  &__text {
    left: 35%;
    top: 25%;
    color: #F5F5F5;
    font-size: 120px;
    font-family: 'Roboto-Condensed-Italic';
  }
}
</style>
