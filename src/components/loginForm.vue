<template>
  <div class="login-container">
    <div class="login">
      <h2 class="login-title">Login</h2>
      <form @submit.prevent="submitForm" class="login-form">
        <div class="form-group">
          <label for="username" class="form-label">
            User
          </label>
          <input
            type="text"
            id="username"
            v-model="username"
            class="form-input"
            placeholder="Enter your username"
            required
          >
        </div>
        <div class="form-group">
          <label for="password" class="form-label">
            Password
          </label>
          <input
            type="password"
            id="password"
            v-model="password"
            class="form-input"
            placeholder="Enter your password"
            required
          >
        </div>
        <p class="register-text">ยังไม่มีบัญชี? <a href="#" @click="showRegister">สร้างบัญชี</a></p>
        <button type="submit" class="login-button">Login</button>
        
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "loginForm",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async submitForm() {
  try {
    const response = await axios.post('https://api.nitirat.co.th/auth/sign-in', {
      username: this.username,
      password: this.password
    });

    console.log('API Response:', response.data); 

    if (response.data.statusCode === 200) {
      const token = response.data.data.access_token;
      localStorage.setItem('access_token', token);
      alert('ล็อกอินสำเร็จ');
    } else {
      alert('มีข้อผิดพลาดในการล็อกอิน: ' + response.data.message);
    }
  } catch (error) {
    console.error('Error:', error);
    alert('เกิดข้อผิดพลาดในการล็อกอิน');
  }
}
  }
};
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Anuphan:wght@200&family=Itim&family=Poppins:ital,wght@1,200&family=Prompt:wght@300&display=swap');
*{
  font-family: 'Itim', cursive;
  padding: auto;
  margin: auto;
  
}
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to bottom, #ddd, #999);
  
}

.login {
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #ffffff;
  width: 300px;
  backdrop-filter: blur(50px); /* เพิ่มเอฟเฟกต์ blur ให้เหมือนกระจกโปร่งใส */
}

.login-title {
  margin-bottom: 15px;
  font-size: 1.5rem;
  color: #333;
  text-align: center;
}

.login-form .form-group {
  margin-bottom: 20px;
}

.form-label {
  display: block;
  font-weight: bold;
  margin-bottom: 8px;
  color: #555;
}

.form-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.register-text {
  margin-top: 10px;
  font-size: 0.9rem;
  color: #555;
  margin:auto;
  padding: 10px;
}

.register-text a {
  color: #4c75a3;
  text-decoration: underline;
  cursor: pointer;
}
.login-button {
  background-color: #4c75a3;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px 15px;
  cursor: pointer;
  width: 100%;
  transition: background-color 0.3s ease-in-out;
  margin-top: 20px;
  display: block;
  margin: 0 auto;
}

.login-button:hover {
  background-color: #304d6d;
}
</style>

