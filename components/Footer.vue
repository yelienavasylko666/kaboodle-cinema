<template>
<div class="footer">
  <img src="../assets/svg/footer-logo.svg" class="footer__logo-left">
  <img src="../assets/svg/footer-logo.svg" class="footer__logo-right">
<h4>Kaboodle</h4>
<div class="footer__links">
  <nuxt-link to="/" class="footer__link">FAQ |</nuxt-link>
  <nuxt-link to="/" class="footer__link">Feedback |</nuxt-link>
  <nuxt-link to="/" class="footer__link">T&Cs |</nuxt-link>
  <nuxt-link to="/" class="footer__link">Privacy Policy</nuxt-link>
</div>
  <div class="footer__copyright">Copyright 2016 - All Rights Reserved</div>
</div>
</template>

<script>
    export default {
        name: "Footer"
    }
</script>

<style  lang="scss">
.footer {
  height: 181px;
  background-color: #000000;
  position: relative;
  overflow: hidden;

h4 {
  font-size: 28px;
  color: #F5F5F5;
  margin-top: 35px;
  text-align: center;
  font-family: 'Roboto-Condensed-Bold-Italic';
}
  &__logo-left {
    position: absolute;
    top: 40px;
    left: -6%;
    width: 33%;
  }

  &__logo-right {
    position: absolute;
    top: -190px;
    right: -17%;
    width: 33%;
  }
  &__links {
    text-align: center;
    margin: 20px 0 30px;
    font-family: 'Roboto-Condensed-Italic';
    font-size: 18px;
  }
  &__link {
    color: #F5F5F5;
    font-size: 24px;
    text-decoration: none;
  }
  &__copyright {
    text-align: center;
    font-size: 18px;
    color: #F5F5F5;
    margin-bottom: 27px;
    font-family: 'Roboto-Condensed-Italic';
  }
}
</style>
