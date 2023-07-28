<template>
    <h1 class="title ">
        <span>&#9728;</span> Validation Form <span>&#9728;</span>
    </h1>
    <form  @submit.prevent="register" >
    <input :class="{'valid': isValidEmail === true , 'invalid': isValidEmail === false }"
     v-model="email" type="text" placeholder="Email.."> <span class="spanCheckEmail" v-if="isValidEmail">&#10003;</span>
      <br>
    <div v-if="email != '' && !isValidEmail">Invalid email address!</div> <br>
    <input :class="{'valid': isStrongPassword === true , 'invalid': isStrongPassword === false }"
     v-model="password" type="password" placeholder="Password.."> <br>
     <div v-if="password != '' && !isStrongPassword">Weak password!</div> <br>
    <input :class="{'valid': isPasswordConfirmed === true , 'invalid': isPasswordConfirmed === false }"
     v-model="confirmPassword" type="password" placeholder="Confirm password"> <br>
    <br>
    <button :disabled="startValidation" type="submit">Register</button>
    </form>
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
    startValidation.value = false;
};

const isValidEmail = computed(() => {   
 return email.value ? /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email.value)
                              : null;
 });

const isStrongPassword = computed(() => {
//* it must include uppercase, lowercase, number, letters,
// special characters, lenght 8 or more, (can includes white space)
 return password.value ? /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9\d])(?=.*\d).{8,}/.test(password.value)
                              : null;
 });

const isPasswordConfirmed = computed(() => {
 return confirmPassword.value ? password.value === confirmPassword.value
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
    background-color: tomato;
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
