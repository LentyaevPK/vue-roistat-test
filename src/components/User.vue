<template>
  <div class="table__group">
    <div class="table__row">
      <span
        v-if="employees.length"
        :class="['table__btn', { 'table__btn--up': showEmployees }]"
        @click="showEmployees = !showEmployees"
      >&#9660;</span>
      <div class="table__username">{{ user.username }}</div>
      <div class="table__tel">+7{{ user.telephone }}</div>
    </div>
    <div v-if="showEmployees">
      <User
        v-for="employee in employees"
        :key="employee.id"
        :user="employee"
        :users="users"
        style="margin-left: 15px"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'User',
  props: {
    user: {
      type: Object,
      required: true,
    },
    users: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      showEmployees: false,
    };
  },
  computed: {
    employees() {
      return this.users.filter((user) => user.chief === this.user.id);
    },
  },
};
</script>

<style></style>
