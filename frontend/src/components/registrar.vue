<script lang="ts">
import { ref } from "vue"

export default {
  name: "Register",
  setup() {
    const fullName = ref("")
    const email = ref("")
    const phone = ref("")
    const password = ref("")
    const confirmPassword = ref("")
    const acceptedTerms = ref(false)

    const handleRegister = () => {
      if (!acceptedTerms.value) {
        alert("Você precisa aceitar a Política de Privacidade.")
        return
      }

      if (password.value !== confirmPassword.value) {
        alert("As senhas não coincidem.")
        return
      }

      console.log({
        fullName: fullName.value,
        email: email.value,
        phone: phone.value,
        password: password.value,
      })
    }

    return {
      fullName,
      email,
      phone,
      password,
      confirmPassword,
      acceptedTerms,
      handleRegister,
    }
  },
}
</script>

<template>
  <div class="register-page">
    <h1>REGISTRE-SE</h1>
    <p class="subtitle">PREENCHA TODOS OS CAMPOS ABAIXO</p>

    <div class="form-box">
      <label>NOME COMPLETO*</label>
      <input v-model="fullName" type="text" placeholder="DIGITE SEU NOME" />

      <div class="row">
        <div>
          <label>EMAIL*</label>
          <input v-model="email" type="email" placeholder="SEUEMAIL@GMAIL.COM" />
        </div>

        <div>
          <label>TELEFONE (OPCIONAL)</label>
          <input v-model="phone" type="tel" placeholder="(99)99999-9999" />
        </div>
      </div>

      <div class="row">
        <div>
          <label>SENHA*</label>
          <input v-model="password" type="password" placeholder="SENHA" />
        </div>

        <div>
          <label>CONFIRMAR SENHA*</label>
          <input
            v-model="confirmPassword"
            type="password"
            placeholder="SENHA"
          />
        </div>
      </div>

      <div class="terms">
        <input type="checkbox" v-model="acceptedTerms" />
        <p>
          Li e aceito a <strong>Política de Privacidade</strong> e autorizo o
          uso dos meus dados conforme a LGPD
        </p>
      </div>

      <small>Campos marcados com (*) são obrigatórios</small>

      <button @click="handleRegister">REGISTRAR</button>
    </div>
  </div>
</template>

<style scoped>
.register-page {
  background: #2f2f2f;
  min-height: 100vh;
  padding: 3rem;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  margin-bottom: 0.3rem;
}

.subtitle {
  opacity: 0.8;
  margin-bottom: 2rem;
}

.form-box {
  width: 850px;
  max-width: 100%;
}

label {
  display: block;
  margin: 1rem 0 0.3rem;
  font-size: 0.9rem;
  opacity: 0.8;
}

input[type="text"],
input[type="password"],
input[type="email"],
input[type="tel"] {
  width: 100%;
  padding: 0.7rem 1rem;
  border-radius: 25px;
  border: 1px solid #ff2c2c;
  outline: none;
}

.row {
  display: flex;
  gap: 1rem;
}

.row div {
  flex: 1;
}

.terms {
  display: flex;
  align-items: center;
  margin-top: 1.5rem;
  gap: 0.5rem;
  font-size: 0.8rem;
}

small {
  display: block;
  margin-top: 0.5rem;
  opacity: 0.7;
}

button {
  margin-top: 2rem;
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
