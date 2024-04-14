<script setup>

import {inject} from "vue";

defineProps({
  number: Number,
  name: String,
  company: String,
  group: String,
  isPresence: Boolean,
  onClickUser: Function,
})

</script>

<template>
  <tr class="table__body-item" @click="onClickUser">
    <td class="table__body-row">{{ number + 1 }}</td>
    <td class="table__body-row">{{ name }}</td>
    <td class="table__body-row">{{ company }}</td>
    <td class="table__body-row">{{ group }}</td>
    <td class="table__body-row">
      <img class="table__body-img" :src="!isPresence ? '../../public/images/marker-false.svg' : '../../public/images/marker-true.svg'" alt="presence">
    </td>
  </tr>
</template>

<style scoped lang="less">
.table {

  &__body-item {
    cursor: pointer;
  }

  &__body-item:hover,
  &__body-item:focus {
    background: #c4c4c4;;
  }

  &__body-row {
    padding-top: 1rem;
    padding-bottom: 1rem;
    color: rgb(0, 0, 0);
    font-size: 1.88rem;
    font-weight: 400;
    line-height: 2.56rem;
    letter-spacing: 0%;
    text-align: left;
  }

  &__body-row:last-child {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__body-img {
    width: 3.69rem;
    height: 3.69rem;
  }
}
</style>