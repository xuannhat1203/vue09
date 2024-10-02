<template>
    <div class="form-container">
        <h3>Register</h3>
        <div class="form-group">
            <label for="full-name">FullName</label>
            <input v-model="products.fullName" type="text" id="full-name">
        </div>
        <div class="form-group">
            <label for="email">Email</label>
            <input v-model="products.email" type="email" id="email">
            <p style="color: red;" v-show="check">Email already exists</p>
        </div>
        <div class="form-group">
            <label for="password">Password</label>
            <input v-model="products.password" type="password" id="password">
        </div>
        <div class="form-group">
            <label for="re-password">Confirm Password</label>
            <input v-model="products.rePassword" type="password" id="re-password">
        </div>
        <p v-show="check2" style="color: red;">Email, FullName or Password cannot be left blank</p>
        <button @click="handleClick">Register</button>
    </div>
</template>


<script setup>
import { ref } from 'vue';
const data = ref(JSON.parse(localStorage.getItem("data")) || []);
const check = ref(false);
const check2 = ref(false); 
const products = ref({
    fullName: "",
    email: "",
    password: "",
    rePassword: "",
});
const handleClick = () => {
    check.value = false;
    check2.value = false;
    const find = data.value.find((user) => user.email === products.value.email);
    if (!products.value.fullName || !products.value.email || !products.value.password) {
        check2.value = true;
        return;
    }

    if (find) {
        check.value = true;
        return;
    }
    data.value.push({ 
        fullName: products.value.fullName, 
        email: products.value.email, 
        password: products.value.password 
    });
    localStorage.setItem("data", JSON.stringify(data.value));
    products.value.fullName = "";
    products.value.email = "";
    products.value.password = "";
    products.value.rePassword = "";
};
</script>
<style>
.form-container {
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

input[type="text"], input[type="number"] {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-size: 16px;
}

input[type="text"]:focus, input[type="number"]:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
}

input[type="text"]::placeholder, input[type="number"]::placeholder {
    color: #aaa;
}

</style>
