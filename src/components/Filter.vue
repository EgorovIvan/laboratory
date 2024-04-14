<script setup>
import {ref} from "vue";

defineProps({
  onChangeSelect: Function
})

</script>

<template>
  <div class="filter">
    <div class="filter__title">
      Фильтровать по:
    </div>

    <input @input="onChangeSelect" type="radio" id="absence" value="absence" name="filter"/>
    <label for="absence" class="filter__text">Отсутствующим</label>

    <input @input="onChangeSelect" type="radio" id="availability" value="availability" name="filter">
    <label for="availability" class="filter__text">Присутствующим</label>

    <input checked @input="onChangeSelect" type="radio" id="nofilter" value="nofilter" name="filter">
    <label for="nofilter" class="filter__text">Без фильтра</label>

  </div>
</template>

<style scoped lang="less">
.filter {
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: start;
  gap: 0.75rem;
  margin: 0 0 2.875rem 3.125rem;
  width: 100%;

  &__title {
    padding: 0.375rem 2.5rem 0.5rem 0;
    color: rgb(78, 48, 0);
    font-size: 1.88rem;
    font-weight: 700;
    line-height: 2.56rem;
    letter-spacing: 0%;
    text-align: left;
  }

  &__text {
    padding: 0.375rem 1.25rem 0.5rem;
    color: rgb(78, 48, 0);
    font-size: 1.56rem;
    font-weight: 400;
    line-height: 2.13rem;
    letter-spacing: 0%;
    text-align: left;
    border-radius: 1.25rem;
    cursor: pointer;
  }
}

input[type="radio"]:checked + label {
  color: rgb(255, 255, 255);
  background: rgb(196, 196, 196);
}

[type="radio"] {
  display: none;
}

</style>