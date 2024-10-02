<template>
    <div class="form-container">
        <h3>Register</h3>
        <div class="form-group">
            <label for="product-code">FullName</label>
            <input value="" v-model="products.code" type="text" id="product-code">
        </div>
        <div class="form-group">
            <label for="product-name">Email</label>
            <input value="" v-model="products.nameProduct" type="text" id="product-name">
        </div>
        <div class="form-group">
            <label for="price">PassWord</label>
            <input value="" v-model="products.price" type="text" id="price">
        </div>
        <div class="form-group">
            <label for="quantity">PassWord</label>
            <input value="" v-model="products.quantity" type="text"  id="quantity">
        </div>
        <button @click="handleClick">Register</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const products = ref({
    fullName: "",
    Email: "",
    PassWord: "",
    RePassWord: "",
})
const handleClick = () => {
    console.log(products.value);
}


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
