<template>
  <form class="form" @submit.prevent="createUser">
    <h2 class="form__header">Добавить пользователя</h2>
    <button class="form__close-btn" @click="$emit('closeForm')">x</button>
    <div class="form__input">
      <label>Имя</label>
      <input type="text" v-model="username" required />
    </div>
    <div class="form__input">
      <label>Телефон</label>
      <input
        type="tel"
        pattern="\([0-9]{3}\)[0-9]{3}-[0-9]{4}"
        v-model="telephone"
        required
      />
      <small class="form__hint">Введите номер в формате: (123)123-1234</small>
    </div>
    <div class="form__input">
      <label>Начальник</label>
      <select class="form__select" v-model="chief" required>
        <option value="none">Нет</option>
        <option v-for="user in users" :key="user.id" :value="user.id">{{
          user.username
        }}</option>
      </select>
    </div>
    <button type="submit" class="button form__submit-btn">Сохранить</button>
  </form>
</template>

<script>
export default {
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      username: null,
      telephone: null,
      chief: null,
    };
  },
  methods: {
    createUser() {
      const user = {
        id: Date.now(),
        username: this.username.trim(),
        telephone: this.telephone.trim(),
      };

      user.chief = this.chief === 'none' ? null : this.chief;

      this.$emit('addUser', user);
      this.username = null;
      this.telephone = null;
      this.chief = null;
    },
  },
};
</script>

<style>
.form {
  position: relative;
  width: 450px;
  background-color: #fff;
  box-shadow: 1px 1px 5px black;
  padding: 20px;
  margin-left: 30px;
}

.form__close-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  background-color: #fff;
  border: none;
  cursor: pointer;
}

.form__header {
  font-size: 1.5rem;
  margin-bottom: 20px;
}

.form__input {
  position: relative;
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 30px;
}

.form__hint {
  position: absolute;
  top: 100%;
  right: 0;
}

.form__input input {
  width: 60%;
}

.form__select {
  display: block;
  width: 60%;
}
</style>
