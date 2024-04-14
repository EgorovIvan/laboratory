<script setup>
import Header from "@/components/Header.vue";
import TableVisitors from "@/components/TableVisitors.vue";
import Filter from "@/components/Filter.vue";
import {onMounted, reactive, ref, watch} from "vue";
import axios from "axios";
import debounce from "lodash.debounce";
import Modal from "@/components/Modal.vue";

const users = ref([]);
const modalUser = ref({});
const showModal = ref(false);
const countAvailability = ref(0);
const countAbsence = ref(0);
const groupList = ref([]);

const filters = reactive({
  filterBy: 'nofilter',
  searchQuery: '',
})

// Группировать списки групп
const groupBy = () => {
  const array = [];

  for (let user of users.value) {
    array.push(user.group);
  }
  groupList.value = array.filter((element, index) =>
      array.indexOf(element) === index
  ).sort();
}

// Выбрать пользователя
const onClickUser = (user) => {
  Object.assign(modalUser.value, user);
  showModal.value = true
}

// Открыть модальное окно
const openModal = () => {
  modalUser.value = {}
  showModal.value = true
}

//Закрыть модальное окно
const closeModal = () => {
  showModal.value = false
  modalUser.value = {}
}

// Выбрать опцию фильтрации
const onChangeSelect = (event) => {
  filters.filterBy = event.target.value;
}

//Поиск
const onChangeSearchInput = debounce((event) => {
  filters.searchQuery = event.target.value;
}, 500);

// Сохранить изменения
const save = async () => {
  const localUsers = localStorage.getItem('users');
  users.value = JSON.parse(localUsers);

  const find = users.value.find((user) => modalUser.value.id === user.id)

  if (find) { // Изменить существующего посетителя
    users.value = users.value.map((user) => {
      if (user.id === modalUser.value.id) {
        return Object.assign(user, modalUser.value);
      } else {
        return user
      }
    })
    localStorage.setItem('users', JSON.stringify(users.value))

  } else { // Добавить нового посетителя
    modalUser.value.id = users.value.length + 1;
    users.value.push(modalUser.value);
    localStorage.setItem('users', JSON.stringify(users.value))
  }
  await closeModal();
  await fetchUsers();
}

// Загрузить посетителей
const fetchUsers = async () => {
  try {

    const localUsers = localStorage.getItem('users');

    users.value = JSON.parse(localUsers);

    // Количество отсутствующих
    countAbsence.value = users.value.filter((user) => {
      if (!user.isPresence) {
        return user
      }
    }).length;

    // Количество присутствующих
    countAvailability.value = users.value.filter((user) => {
      if (!!user.isPresence) {
        return user
      }
    }).length;

    // Фильтрация
    switch (filters.filterBy) {
      case 'absence':
        users.value = users.value.filter((user) => {
          if (!user.isPresence) {
            return user;
          }
        });
        break;
      case 'availability':
        users.value = users.value.filter((user) => {
          if (!!user.isPresence) {
            return user;
          }
        })
        break;
      default:
        users.value;
    }

    // Поиск по имени
    users.value = users.value.filter((user) => {
      const found = user.name.toLowerCase().includes(filters.searchQuery.toLowerCase());
      if (found) {
        return user;
      }
    })

  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  const {data} = await axios.get('../public/users.json')
  localStorage.setItem('users', JSON.stringify(data))

  await fetchUsers();
  await groupBy();
})

watch(filters, fetchUsers)

</script>

<template>
  <div class="container">
    <Header
        :on-change-search-input="onChangeSearchInput"
        :open-modal="openModal"
        :count-availability="countAvailability"
        :count-absence="countAbsence"
    />

    <TableVisitors
        :users="users"
        @on-click-user="onClickUser"
    />

    <Modal
        v-show="showModal"
        :show-modal="showModal"
        :group-list="groupList"
        :modal-user="modalUser"
        :save="save"
        :close-modal="closeModal"
    />

    <Filter
        :on-change-select="onChangeSelect"
    />
  </div>
</template>

<style scoped lang="less">
.container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
  width: 121.75rem;
  margin: 0 auto;
  padding-top: 1.5rem;

}
</style>
