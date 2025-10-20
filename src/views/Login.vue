<template>
  <div class="login-page">
    <div class="login-container">
      <h1>Belépés</h1>
      <form @submit.prevent="handleLogin">
        <div class="form-group">
          <label for="email">Email</label>
          <input
            id="email"
            type="email"
            v-model="email"
            placeholder="Írd be az emailed"
            required
          />
        </div>
        <div class="form-group">
          <label for="password">Jelszó</label>
          <input
            id="password"
            type="password"
            v-model="password"
            placeholder="Írd be a jelszavad"
            required
          />
        </div>
        <button type="submit" class="login-button">Bejelentkezés</button>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
        <p class="switch-link">
          Nincs még fiókod? <router-link to="/">Regisztráció</router-link>
        </p>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',
      errorMessage: ''
    }
  },
  methods: {
    async handleLogin() {
      try {
        const response = await axios.post('https://localhost:7262/api/Auth/login', {
          email: this.email,
          password: this.password
        })
        const user = response.data
        localStorage.setItem('user', JSON.stringify(user))
        this.$router.push('/dashboard')
      } catch (error) {
        console.error(error)
        this.errorMessage =
          error.response?.data?.message || 'Hibás email vagy jelszó'
      }
    }
  }
}
</script>

<style scoped>
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(to right, #4facfe, #00f2fe);
  padding: 20px;
}

.login-container {
  width: 100%;
  max-width: 400px;
  background: #fff;
  border-radius: 12px;
  padding: 30px 25px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
}

h1 {
  text-align: center;
  margin-bottom: 25px;
  color: #333;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  margin-bottom: 8px;
  font-weight: 500;
  color: #555;
}

input {
  padding: 12px 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
  transition: all 0.2s;
}

input:focus {
  border-color: #4facfe;
  box-shadow: 0 0 8px rgba(79, 172, 254, 0.3);
  outline: none;
}

.login-button {
  width: 100%;
  padding: 12px;
  background-color: #4facfe;
  color: #fff;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s;
}

.login-button:hover {
  background-color: #00f2fe;
}

.error {
  margin-top: 15px;
  color: #ff4d4f;
  text-align: center;
  font-weight: 500;
  font-size: 14px;
}

.switch-link {
  margin-top: 15px;
  text-align: center;
  font-size: 14px;
}

/* Mobilbarát */
@media (max-width: 480px) {
  .login-container {
    padding: 25px 20px;
  }

  input,
  .login-button {
    font-size: 14px;
    padding: 10px;
  }
}
</style>
