<template>
  <div class="login-page" v-if="user">
    <div class="login-container">
      <h1>Üdv, {{ user.name }}!</h1>
      <p class="role">Szereped: <span>{{ user.role }}</span></p>
      <button @click="logout" class="login-button logout-button">Kijelentkezés</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data() {
    return {
      user: null
    }
  },
  created() {
    const storedUser = localStorage.getItem('user')
    if (storedUser) {
      this.user = JSON.parse(storedUser)
    } else {
      this.$router.push('/login')
    }
  },
  methods: {
    logout() {
      localStorage.removeItem('user')
      this.$router.push('/login')
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
  text-align: center;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
}

h1 {
  text-align: center;
  margin-bottom: 15px;
  color: #333;
}

.role {
  font-size: 16px;
  color: #555;
  margin-bottom: 25px;
}

.role span {
  font-weight: 600;
  color: #4facfe;
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

.logout-button {
  background-color: #ff4d4f;
  margin-top: 10px;
}

.logout-button:hover {
  background-color: #ff7875;
}

.login-button:hover:not(.logout-button) {
  background-color: #00f2fe;
}

/* Mobilbarát */
@media (max-width: 480px) {
  .login-container {
    padding: 25px 20px;
  }

  .login-button {
    font-size: 14px;
    padding: 10px;
  }
}
</style>
