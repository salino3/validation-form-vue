<!--
78UU+*yy 
-->
<template>
    <h1 class="title"><span>&#9728;</span> Validation User Form <span>&#9728;</span></h1>
    <form class="myForm"  @submit.prevent="register">
    <input :class="{'valid': isValidEmail === true, 'invalid': isValidEmail === false || (startValidationColor.email && !isValidEmail)}"
     v-model="user.email" type="text" placeholder="Email..">
      <br>
    <span class="errorText" v-if="user.email != '' && !isValidEmail ">Invalid email address!</span> <br>

    <input :class="{'valid': isStrongPassword === true , 'invalid': isStrongPassword === false  || (startValidationColor.password && !isStrongPassword)}"
     v-model="user.password" type="password" placeholder="Password.."> <br>
     <span class="errorText"  v-if="user.password != '' && !isStrongPassword">Weak password!</span> <br>
    <input  :class="{ 'passwordConfirmed': user.password != user.confirmPassword ,
         'valid': isPasswordConfirmed === true , 'invalid': isPasswordConfirmed === false || (startValidationColor.confirmPassword && !isPasswordConfirmed)}"
     v-model="user.confirmPassword" type="password" placeholder="Confirm password"> <br>
     <span class="errorText" v-if="user.confirmPassword != '' && !isPasswordConfirmed">Repeat password!</span>
    <br> 
    <!--  -->
    <input :class="{'valid': user.age >= 18 , 'invalid': isMajor === false || (startValidationColor.age && !isMajor || (user.age != null && !isMajor && user.age < 18))}"
     type="number"  min="0" v-model="user.age" placeholder="Age.."  > <br>
     <span class="errorText" v-if="user.age != null && !isMajor && user.age < 18">You must be Major!</span>
     <br>
      <div>
        <label for="dev">What developer are you?</label> &nbsp; 
        <select v-model="user.dev" id="dev">
            <option value="">..</option>
            <option value="Front-end">Front-end</option>
            <option value="Back-end">Back-end</option>
            <option value="DevOps">DevOps</option>
        </select> 
     </div>
      <br>
     <div>
        <p>Your sex:</p>
        <label for="Male">Male</label>
         <input v-model="isMaleChecked"
          id="Male" type="checkbox" class="inputCheckBox"  @change="onChangeSex('Male')">
         &nbsp;
          <label for="Famel">Famale</label> 
         <input v-model="isFemaleChecked"
          type="checkbox" class="inputCheckBox"  @change="onChangeSex('Female')">
     </div>
    <br>
    <button type="submit" :disabled="startValidation" >Register</button>
    </form>
</template>

<script setup>
import {ref, reactive, computed} from 'vue';

const startValidation = ref(false);
const startValidationColor = reactive({
    email: false,
    password: false,
    confirmPassword: false,
    age: false, 
    sex: false,
    dev: false

});

const user = reactive({
    email: "",
    password: "",
    confirmPassword: "",
    age: null, 
    sex: "",
    dev: ""

});

//
const isMaleChecked = ref(false);
const isFemaleChecked = ref(false);

const onChangeSex = (sex) => {
if (sex === 'Male') {
    user.sex = 'Male';
    isMaleChecked.value = true;
    isFemaleChecked.value = false;
  };
  if (sex === 'Female') {
    user.sex = 'Female';
    isMaleChecked.value = false;
    isFemaleChecked.value = true;
  };
};

function register() {
    startValidation.value = true;
    startValidationColor.email = true;
    startValidationColor.password = true;
    startValidationColor.confirmPassword = true;
    startValidationColor.age = true;
    startValidationColor.sex = true;
    startValidationColor.dev = true;


    if (isValidEmail.value === true && isStrongPassword.value === true
     && isPasswordConfirmed.value === true && isMajor.value === true
     && user.sex && user.dev ) {
        alert("Registering...");
   console.log(JSON.stringify(user, null, 2));
    }else {
      alert("You have some error in the Form...");
      console.log(user);
    };
      startValidation.value = true;
      
};

const isValidEmail = computed(() => {   
 
  if(user.email != ""){
    startValidationColor.email = true;
  };

 return user.email ? /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(user.email) : null;
 });
    
const isStrongPassword = computed(() => {

    if(user.password != ""){
    startValidationColor.password = true;
  };
//* it must include uppercase, lowercase, number, letters,
// special characters, lenght 8 or more, (can includes white space)
 return user.password ? /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9\d])(?=.*\d).{8,}/.test(user.password)
                              : null;
 });

const isPasswordConfirmed = computed(() => {

   if(user.confirmPassword != "" && user.password != user.confirmPassword){
   startValidationColor.confirmPassword = true;
  }
  
 return user.confirmPassword ? user.password === user.confirmPassword
                              : null;
 });

 const isMajor = computed(() => {

  if(user.age != null){
    startValidationColor.age = false;
  }

 return startValidation.value ? user.age >= 18
                              : null;
 });


</script>

<style lang="css" scope>

.muForm input{
  
    border-radius: 8px;
    padding: 3px;
    align-self: center;
}

.myForm button {
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: 18px;
  color:blue;
  background: rgb(232, 208, 208);;
  border-radius: 8px;
  padding: 4px;
  margin-top: 20px;
}

.myForm {
  border: solid rgb(38, 132, 38, 0.7) 3px;
  border-radius: 10px;
  padding: 18px 12px;
  display: flex;
  flex-direction: column;
}

.title{
    font-size: 26px;
    color: orange;
}

.title > span {
  color: rgb(238, 238, 17);
}

.passwordConfirmed:focus {
    background: url('/icons8-x-16.png') no-repeat right;
    background-color: tomato;
    background-size: 20px 20px;
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

.errorText {
  color: red;
}

</style>




