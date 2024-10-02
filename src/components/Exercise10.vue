<template>
    <div class="login-container">
      <h3>Login</h3>
      <div class="form-group">
        <label for="email">Email</label>
        <input v-model="email" type="email" id="email" placeholder="Enter your email">
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input v-model="password" type="password" id="password" placeholder="Enter your password">
      </div>
      <p v-show="error" style="color: red;">Incorrect email or password</p>
      <button @click="handleLogin">Login</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  const users = ref(JSON.parse(localStorage.getItem("data")) || []);
  const email = ref(""); 
  const password = ref(""); 
  const error = ref(false); 
  
  const handleLogin = () => {
    error.value = false;
  
    const user = users.value.find(user => user.email === email.value && user.password === password.value);
  
    if (user) {
      alert("Login successful!");
    } else {
      error.value = true; 
    }
  };
  </script>
  

  <style>
  .login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
  }
  
  h3 {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #555;
  }
  
  input[type="email"], input[type="password"] {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-size: 16px;
  }
  
  input:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
  }
  
  input::placeholder {
    color: #aaa;
  }
  
  button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  </style>
  