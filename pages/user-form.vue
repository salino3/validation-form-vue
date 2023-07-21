
<template>
    <h1 class="title"><span>&#9728;</span> Validation User Form <span>&#9728;</span></h1>
    <div>
    <input :class="{'valid': isValidEmail === true , 'invalid': isValidEmail === false }"
     v-model="user.email" type="text" placeholder="Email.."> <span class="spanCheckEmail" v-if="isValidEmail">&#10003;</span>
      <br>
    <div  v-if="user.email != '' && !isValidEmail && isValidEmail.valueOf(null) ">Invalid email address!</div> <br>
    <input :class="{'valid': isStrongPassword === true , 'invalid': isStrongPassword === false }"
     v-model="user.password" type="text" placeholder="Password.."> <br>
     <div v-if="user.password != '' && !isStrongPassword">Weak password!</div> <br>
    <input :class="{'valid': isPasswordConfirmed === true , 'invalid': isPasswordConfirmed === false }"
     v-model="user.confirmPassword" type="text" placeholder="Confirm password"> <br>
    <br> 
    <!--  -->
    <input :class="{'valid': isMajor === true, 'invalid': isMajor === false}"
     type="number" v-model="user.age" placeholder="Age.."  > <br>
     <div v-if="user.age != null && !isMajor && user.age < 18">You must be Major!</div>
     <br>

    <br>
    <button @click="register">Register</button>
 </div>
  <li>
    <nuxt-link to="/">
        Go to Home
    </nuxt-link>
  </li>
</template>

<script setup>
import {ref, reactive, computed, watch} from 'vue';

const startValidation = ref(false);
const startValidationColor = ref(false);

const user = reactive({
    email: "",
    password: "",
    confirmPassword: "",
    age: null, 
    sex: "",
    spanish: null

});


// const email = ref('');
// const password = ref('');
// const confirmPassword = ref('');

function register() {
    startValidation.value = true;
    startValidationColor.value = true;

    if (isValidEmail.value === true && isStrongPassword.value === true
     && isPasswordConfirmed.value === true && isMajor.value === true) {
        alert("Registering...");
    };
};

const isValidEmail = computed(() => {   
 return startValidation.value ? /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(user.email)
                              : null;
 });
    
const isStrongPassword = computed(() => {
//* it must include uppercase, lowercase, number, letters,
// special characters, lenght 8 or more, (can includes white space)
 return startValidation.value ? /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9\d])(?=.*\d).{8,}/.test(user.password)
                              : null;
 });

const isPasswordConfirmed = computed(() => {
 return startValidation.value ? user.password === user.confirmPassword
                              : null;
 });

 const isMajor = computed(() => {
 return startValidation.value ? user.age >= 18
                              : null;
 });


// Watcher para actualizar las propiedades computadas cuando cambian los valores del input
// watch(
//   () => user.email,
//   () => {
//     if (startValidation.value) {
//       isValidEmail.value = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(
//         user.email
//       );
//     }
//   }
// );

// watch(
//   () => user.password,
//   () => {
//     if (startValidation.value) {
//       isStrongPassword.value = /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9\d])(?=.*\d).{8,}/.test(
//         user.password
//       );
//     }
//   }
// );

// watch(
//   () => user.confirmPassword,
//   () => {
//     if (startValidation.value) {
//       isPasswordConfirmed.value = user.password === user.confirmPassword;
//     }
//   }
// );

// watch(
//   () => user.age,
//   () => {
//     if (startValidation.value) {
//       isMajor.value = user.age >= 18;
//     }
//   }
// );


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




