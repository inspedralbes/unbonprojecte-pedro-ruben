<template>
  <div>
    <h1>CRUD</h1>
    <form @submit.prevent="addUser">
      <input v-model="newUser.name" placeholder="Nombre" />
      <input v-model="newUser.email" placeholder="Email" />
      <button type="submit">Agregar usuario</button>
    </form>
    <ul>
      <li v-for="(user, index) in users" :key="index">
        {{ user.name }} - {{ user.email }}
        <button @click="editUser(index)">Editar</button>
        <button @click="deleteUser(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      newUser: {
        name: '',
        email: ''
      },
      editIndex: -1
    }
  },
  methods: {
    addUser() {
      if (this.editIndex === -1) {
        this.users.push(this.newUser)
      } else {
        this.users.splice(this.editIndex, 1, this.newUser)
        this.editIndex = -1
      }
      this.newUser = { name: '', email: '' }
    },
    editUser(index) {
      this.newUser = { ...this.users[index] }
      this.editIndex = index
    },
    deleteUser(index) {
      this.users.splice(index, 1)
    }
  }
}
</script>

<style scoped>
h1 {
  color: #333;
  text-align: center;
}

form {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  padding: 10px 20px;
  border-radius: 5px;
  border: none;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
