<script setup>
import TableItem from "@/components/TableItem.vue";

defineProps({
  users: Array,
})

const emit = defineEmits(['onClickUser'])
</script>

<template>
  <table class="table">
    <thead class="table__head">
    <tr  class="table__head-item">
      <th class="table__head-col" style="width: 11%;">Номер</th>
      <th class="table__head-col" style="width: 27%;">ФИО</th>
      <th class="table__head-col" style="width: 21%;">Компания</th>
      <th class="table__head-col" style="width: 31%;">Группа</th>
      <th class="table__head-col" style="width: 10%;">Присутствие</th>
    </tr>
    </thead>
    <hr>
      <tbody class="table__body" v-auto-animate>
      <TableItem
          v-for="(user, number) in users"
          :key="user.id"
          :number="number"
          :name="user.name"
          :company="user.company"
          :group="user.group"
          :isPresence="user.isPresence"
          :onClickUser="() => emit('onClickUser', user)"
      />
      </tbody>
  </table>
</template>

<style scoped lang="less">

.table {
  width: 100%;
  border-collapse: collapse;

  &__head-col {
    padding-bottom: 0.5rem;
    color: rgb(78, 48, 0);
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.69rem;
    text-align: left;
    border-bottom: 0.25rem solid rgb(233, 233, 233);
  }

  &__head-col:last-child {
    text-align: center;
  }

}

hr {
  width: 100%;
  height: 1rem;
  border: none;
  background: none;
}

</style>