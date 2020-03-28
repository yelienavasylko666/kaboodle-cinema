<template>
  <div>
    <header class="header">
      <div class="header__left">
        <img src="../assets/svg/header-logo.svg" class="header__img">
        <div class="header__name">Kaboodle</div>
        <div class="header__desc">DISCOVER AND SHARE MOVIES AND TV SHOWS WITH YOUR FRIENDS</div>
      </div>
      <div class="header__right">
        <div class="header__right-item">
          <img src="../assets/svg/user.svg" class="header__right-logo" alt="img">
          <div class="header__right-info">Sign up</div>
        </div>
        <div class="header__right-item">
          <img src="../assets/svg/user-2.svg" class="header__right-logo" alt="img">
          <div class="header__right-info">Log in</div>
        </div>
        <div class="header__right-item">
          <img src="../assets/svg/about.svg" class="header__right-logo" alt="img">
          <div class="header__right-info">About</div>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style lang="scss">
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #389ef2;
    height: 60px;
    padding: 12px 115px;

    &__img {
      height: 33px;
    }


    &__left,
    &__right {
      color: white;
      display: flex;
      justify-content: space-between;
      }

    &__left {
      flex-grow: 1;
      justify-content: flex-start;
      align-items: center;
    }

    &__name {
      font-size: 24px;
      font-family: 'Roboto-Condensed-Bold-Italic';
      padding: 0 12px;
    }
    &__desc {
      font-family: 'Roboto-Condensed-Bold';
      padding-left: 12px;
      border-left: 2px solid #ffc107;
      font-size: 12px;
      line-height: 33px;
    }
    &__right {
      &-item {
        margin-left: 50px;
        align-items: center;
        transition: 0.3s ease-out;
        cursor: pointer;
      }
      &-item:hover {
        transform: scale(1.1);
      }
      &-logo,
      &-info {
        display: inline-block;
      }
      &-logo {
        height: 16px;
        color: #F5F5F5;
        margin-right: 10px;
      }

      &-info {
        font-size: 20px;
        font-family: 'Roboto-Condensed-Bold';
      }

    }

  }
</style>
