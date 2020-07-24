<template>
  <div class="layout">
    <div class="table">
      <div class="table__row">
        <div class="table__username"><strong class="clickable" @click="sortByField('username')">Имя</strong></div>
        <div class="table__tel"><strong class="clickable" @click="sortByField('telephone')">Телефон</strong></div>
      </div>
      <User v-for="user in chiefs" :key="user.id" :user="user" :users="users" />
      <p v-if="!users.length">Вы не добавили пользователей!</p>
      <button class="button" @click="openForm" :disabled="showForm">
        Добавить
      </button>
    </div>
    <Form
      v-if="showForm"
      @closeForm="closeForm"
      :users="users"
      @addUser="addUser"
    />
  </div>
</template>

<script>
import Form from './components/Form.vue';
import User from './components/User.vue';

export default {
  components: {
    Form,
    User,
  },
  mounted() {
    this.users = JSON.parse(localStorage.getItem('users')) || [];
  },
  data() {
    return {
      showForm: false,
      users: [],
    };
  },
  computed: {
    chiefs() {
      return this.users.filter(user => !user.chief);
    },
  },
  methods: {
    closeForm() {
      this.showForm = false;
    },
    openForm() {
      this.showForm = true;
    },
    addUser(user) {
      this.users.push(user);
      localStorage.setItem('users', JSON.stringify(this.users));
    },
    sortByField(field) {
      this.users.sort((a, b) => {
        if (a[field] > b[field]) {
          return 1;
        }
        if (a[field] < b[field]) {
          return -1;
        }
        return 0;
      });
    },
  },
};
</script>

<style>
.layout {
  width: 100%;
  height: 100vh;
  background-color: rgb(212, 212, 212);
  display: flex;
  justify-content: center;
  align-items: center;
}

.table {
  width: 450px;
  background-color: #fff;
  box-shadow: 1px 1px 5px black;
  padding: 20px;
  margin-right: 30px;
}

.table__row {
  padding: 5px;
  display: flex;
  border-bottom: 1px solid black;
  margin-bottom: 10px;
}

.table__username {
  width: 35%;
}

.table__tel {
  width: 65%;
}

.table__btn {
  margin-right: 5px;
  cursor: pointer;
  transition: 0.3s;
}

.table__btn--up {
  transform: rotate(180deg);
}

.button {
  margin-top: 20px;
  background-color: blue;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px;
  font-size: 16px;
  cursor: pointer;
}

.clickable {
  cursor: pointer;
}
</style>
