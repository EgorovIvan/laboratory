<script setup>

defineProps({
  showModal: Boolean,
  groupList: Array,
  modalUser: Object,
  save: Function,
  closeModal: Function,
})

</script>

<template>
<div class="modal">
  <div class="modal__form">
    <div class="modal__close" @click="closeModal"></div>
    <div class="modal__text">ФИО</div>
    <input type="text" v-model="modalUser.name">
    <div class="modal__text">Компания</div>
    <input type="text" v-model="modalUser.company">
    <div class="modal__text">Группа</div>
    <select v-model="modalUser.group">
      <option disabled value="">Выбрать</option>
      <option
          v-for="item in groupList"
          :key="item"
          :selected="item === modalUser.group"
      >
        {{ item }}
      </option>
    </select>
    <div class="modal__text">Присутствие</div>

    <label for="check" class="modal__check">
      <input type="checkbox" id="check" v-model="modalUser.isPresence">
    </label>
    <div class="modal__block">
      <button type="button" class="modal__btn" @click="save">Добавить</button>
      <div class="modal__btn" @click="closeModal">Закрыть</div>
    </div>
  </div>

</div>
</template>

<style scoped lang="less">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: 5;

  &__close {
    position: absolute;
    width: 2.88rem;
    height: 2.88rem;
    top: 1.25rem;
    right: 1.25rem;
    background: url(../../public/images/close.svg) no-repeat;
    background-size: cover;
    cursor: pointer;
  }

  &__close:hover {
    filter: brightness(1.25);
    transition: filter .2s;
  }

  &__form {
    position: absolute;
    display: grid;
    grid-template-columns: 16rem 31.38rem;
    gap: 2rem 1rem;
    align-items: center;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 91.31rem;
    height: 36.31rem;
    padding: 4rem 0 3rem 26rem;
    box-sizing: border-box;
    border-radius: 1.88rem;
    background: rgb(255, 255, 255);
    z-index: 10;
  }

  &__text {
    color: rgb(78, 48, 0);
    font-size: 2rem;
    font-weight: 600;
    line-height: 2.75rem;
    letter-spacing: 0%;
    text-align: left;
  }

  &__form input[type='text'],
  &__form select {
    width: 31.38rem;
    height: 3.25rem;
    padding: 0 0.5rem;
    border: none;
    outline: none;
    box-shadow: 0rem 0.06rem 0.25rem 0rem rgba(0, 0, 0, 0.16);
    background: rgb(255, 255, 255);
  }

  &__form select {
    cursor: pointer;
  }

  &__check input {
    display: flex;
    align-self: center;
    width: 2rem;
    height: 2rem;
    border: 0.13rem solid rgb(117, 117, 117);
  }

  &__block {
    grid-column-start: 1;
    grid-column-end: 3;
    display: flex;
    gap: 2rem;
    padding-left: 0.5rem;
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
    z-index: -1;
  }

  &__btn:first-child {
    background: url(../../public/images/button-add.png) no-repeat;
    background-size: cover;
  }

  &__btn:last-child {
    background: url(../../public/images/button-close.png) no-repeat;
    background-size: cover;
  }

  &__btn:first-child::before {
    background: url(../../public/images/button-add.png) no-repeat;
    background-size: cover;
  }

  &__btn:last-child::before {
    background: url(../../public/images/button-close.png) no-repeat;
    background-size: cover;
  }

  &__btn:hover {
    filter: brightness(1.25);
    transition: filter .2s;
  }
}


</style>