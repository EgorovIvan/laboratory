<script setup>

defineProps({
  onChangeSearchInput: Function,
  openModal: Function,
  countAvailability: Number,
  countAbsence: Number,
})


</script>

<template>
  <header class="header">
    <div class="header__block">
      <div class="header__logo"></div>
      <input @input="onChangeSearchInput" type="text" placeholder="Поиск по имени" class="header__search">
      <div type="button" class="header__btn" @click="openModal">Добавить</div>
    </div>
    <div class="header__visitors">
      <div class="header__visitors-title">Посетители</div>
      <div class="header__visitors-count">
        <span>{{ countAvailability }}</span> / <span>{{ countAbsence }}</span>
      </div>
    </div>
  </header>
</template>

<style scoped lang="less">
.header {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 2rem;

  &__block {
    display: flex;
    align-items: end;
    justify-content: start;
    gap: 2rem;
  }

  &__logo {
    width: 11.74rem;
    height: 5.59rem;
    background: url(../../public/images/logo.png) no-repeat;
    background-size: contain;
    cursor: pointer;
  }

  &__search {
    width: 24.63rem;
    height: 3.25rem;
    margin-right: 0.5rem;
    padding: 0.9375rem 1.25rem;
    border: none;
    outline: none;
    box-shadow: 0rem 0.06rem 0.25rem 0rem rgba(0, 0, 0, 0.16);
    background: rgb(255, 255, 255);
  }

  &__btn {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 17.06rem;
    height: 3.25rem;
    color: rgb(255, 255, 255);
    font-family: 'Roboto', sans-serif;
    font-size: 1.5rem;
    font-weight: 400;
    line-height: 1.75rem;
    text-align: left;
    border: none;
    background: url(../../public/images/button-add.png) no-repeat;
    background-size: cover;
    cursor: pointer;
  }

  &__btn::before {
    content: '';
    position: absolute;
    width: 16.56rem;
    height: 3.25rem;
    top: 50%;
    left: 50%;
    border-radius: 0.375rem;
    transform: translate(-50%, -50%);
    box-shadow: 0rem 0.19rem 0.19rem 0rem rgba(0, 0, 0, 0.16);
    background: url(../../public/images/button-add.png) no-repeat;
    background-size: cover;
    z-index: -1;
  }

  &__btn:hover {
    filter: brightness(1.25);
    transition: filter .2s;
  }

  &__visitors {
    display: flex;
    flex-direction: column;
    align-items: end;
    justify-content: center;
    gap: 0.25rem;
  }

  &__visitors-title {
    color: rgb(78, 48, 0);
    font-size: 1.88rem;
    font-weight: 700;
    line-height: 2.56rem;
    letter-spacing: 0%;
    text-align: right;
  }

  &__visitors-count {
    color: rgb(78, 48, 0);
    font-size: 1.88rem;
    font-weight: 700;
    line-height: 2.56rem;
    letter-spacing: 0%;
    text-align: right;
  }

  &__visitors-count span:nth-child(1) {
    color: rgb(128, 187, 0);
  }

  &__visitors-count span:nth-child(2) {
    color: rgb(236, 89, 55);
  }

}
</style>