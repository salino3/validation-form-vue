<template>
    <h1 class="title"><span>&#9728;</span> Validation Form <span>&#9728;</span></h1>

    <div>
    <input :class="{'valid': isValidEmail === true , 'invalid': isValidEmail === false }"
     v-model="email" type="text" placeholder="Email.."> <span class="spanCheckEmail" v-if="isValidEmail">&#10003;</span>
      <br>
    <div v-if="email != '' && !isValidEmail">Invalid email address!</div> <br>
    <input :class="{'valid': isStrongPassword === true , 'invalid': isStrongPassword === false }"
     v-model="password" type="text" placeholder="Password.."> <br>
     <div v-if="password != '' && !isStrongPassword">Weak password!</div> <br>
    <input :class="{'valid': isPasswordConfirmed === true , 'invalid': isPasswordConfirmed === false }"
     v-model="confirmPassword" type="text" placeholder="Confirm password"> <br>
    <br>
    <button @click="register">Register</button>
 </div>
</template>

<script setup>
import {ref, computed} from 'vue';

const startValidation = ref(false);

const email = ref('');
const password = ref('');
const confirmPassword = ref('');

function register() {
    startValidation.value = true;

    if (isValidEmail.value === true && isStrongPassword.value === true && isPasswordConfirmed.value === true) {
        alert("Registering...");
    };
};

const isValidEmail = computed(() => {   
 return startValidation.value ? /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email.value)
                              : null;
 });

const isStrongPassword = computed(() => {
//* it must include uppercase, lowercase, number, letters,
// special characters, lenght 8 or more, (can includes white space)
 return startValidation.value ? /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9\d])(?=.*\d).{8,}/.test(password.value)
                              : null;
 });

const isPasswordConfirmed = computed(() => {
 return startValidation.value ? password.value === confirmPassword.value
                              : null;
 });
</script>

<style lang="css" scope>

.title{
    font-size: 26px;
    color: orange;
}

.title > span {
  color: rgb(238, 238, 17);
}

.valid {
    background: url('emblemok_103757.svg') no-repeat right;
    background-size: auto 100%;
    background-color: aqua;
}

.invalid {
    background: url('/icons8-x-16.png') no-repeat right;
    background-color: red;
    background-size: 20px 20px;
}

.spanCheckEmail {
 display: inline-block;
  width: 15px;
  height: 15px;
  background-color: #4CAF50; 
  color: white;
  border-radius: 5px;
  padding: 0px 3px 8px 3px;
  text-align: center;
  justify-content: center;
  }
</style>
