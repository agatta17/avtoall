<template>
  <div id="app">
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
      <tbody v-for="user in users" :key="user.id">
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
      users: userData
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
