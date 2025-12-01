<script lang="ts">
import { ref } from "vue"

export default {
  name: "Login",
  setup() {
    const user = ref("")
    const password = ref("")

    const handleLogin = () => {
      console.log({
        user: user.value,
        password: password.value,
      })
    }

    return {
      user,
      password,
      handleLogin,
    }
  },
}
</script>

<template>
  <div class="login-page">
    <h1>LOGIN</h1>

    <div class="login-box">
      <label>EMAIL OU NOME COMPLETO</label>
      <input v-model="user" type="text" placeholder="DIGITE SEU NOME" />

      <label>SENHA</label>
      <input v-model="password" type="password" placeholder="SENHA" />

      <button @click="handleLogin">CONFIRMAR AGENDAMENTO</button>
    </div>
  </div>
</template>

<style scoped>
.login-page {
  background: #2f2f2f;
  min-height: 100vh;
  padding: 3rem;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.login-box {
  background: #3a3d44;
  padding: 2.5rem;
  border-radius: 50px;
  width: 850px;
  max-width: 100%;
  margin-top: 2rem;
}

label {
  display: block;
  margin: 1.3rem 0 0.4rem;
  font-size: 0.9rem;
  opacity: 0.8;
}

input {
  width: 100%;
  padding: 0.7rem 1rem;
  border-radius: 25px;
  border: 1px solid #3f4cff;
  outline: none;
}

button {
  margin-top: 2.5rem;
  padding: 0.8rem 3rem;
  border-radius: 30px;
  border: none;
  background: #ff2c2c;
  color: white;
  font-weight: bold;
  cursor: pointer;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

button:hover {
  opacity: 0.9;
}
</style>
