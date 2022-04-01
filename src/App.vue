<template>
  <div id="app">
    <form class="form-inline mb-2 ml-2">
      <div class="form-group mr-4">
        <label for="gender" class="mr-2">Пол</label>
        <select class="form-control" id="gender" v-model="filters.gender" @change="filterUsers">
          <option value="all">Все</option>
          <option value="male">Мужчина</option>
          <option value="female">Женщина</option>
        </select>
      </div>
      <div class="mr-2">Возраст:</div>
      <div class="form-group mr-2">
        <label for="minAge" class="mr-2">от</label>
        <input type="number" class="form-control" id="minAge" v-model="filters.age.min" @change="filterUsers">
      </div>
      <div class="form-group">
        <label for="maxAge" class="mr-2">до</label>
        <input type="number" class="form-control" id="maxAge" v-model="filters.age.max" @change="filterUsers">
      </div>
    </form>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Возраст</th>
          <th>Имя</th>
          <th>Пол</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody v-for="user in filteredUsers" :key="user._id">
        <tr>
          <th>{{user._id}}</th>
          <td>{{user.age}}</td>
          <td>{{user.name}}</td>
          <td>{{user.gender}}</td>
          <td>{{user.email}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
const userData = require('@/users.json')


export default {
  name: 'App',
  data() {
    return {
      users: userData,
      filteredUsers: userData,
      filters: {
        gender: 'all',
        age: {
          min: null,
          max: null
        }
      }
    }
  },
  methods: {
    applyGenderFilter(array) {
      if (this.filters.gender !== 'all') {
        return array.filter(item => item.gender.trim() === this.filters.gender); 
      }
    },
    applyMinAgeFilter(array) {
      if (this.filters.age.min) {
        return array.filter(item => item.age > this.filters.age.min)
      }
      return array
    },
    applyMaxAgeFilter(array) {
      if (this.filters.age.max) {
        return array.filter(item => item.age < this.filters.age.max)
      }
      return array
    },
    filterUsers() {
      // TODO: сделать валидацию
      let result = this.users;
      result = this.applyGenderFilter(result);
      result = this.applyMinAgeFilter(result);
      result = this.applyMaxAgeFilter(result);
      this.filteredUsers = result;
    },
  }
}
</script>

<style>
#app {
  width: 80%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 40px auto;
}
</style>
