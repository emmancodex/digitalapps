<template>
  <div class="cont px-4 py-6 bg-light-blue-lighten-3">
    <div
      width="100%"
      max-width="400px"
      class="head mx-auto d-flex justify-left"
    >
      <span class="text-primary text-center pa-4"
        >Welcom to Digital Banking</span
      >
    </div>
    <div
      id="vsheet"
      width="100%"
      class="v-sheet mx-auto d-flex justify-center flex-column ga-2 pa-5"
    >
      <span class="text-h6 signinText pa-2">
        <span class="material-symbols-outlined">lock</span>
        Sign In
      </span>
      <v-form id="form" @submit.prevent="submit" class="ga-4">
        <div class="form-group d-flex flex-column ga-2">
          <div class="text-subtitle-1 d-flex align-center ga-2">
            Username <span class="material-symbols-outlined"> help </span>
          </div>
          <v-text-field
            type="email"
            v-model="formData.username"
            @input="v$.username.$touch"
            @blur="v$.username.$touch"
            :error-messages="v$.username.$errors.map((e) => e.$message)"
            required
            density="compact"
            variant="outlined"
          ></v-text-field>
        </div>

        <div class="form-group d-flex flex-column ga-2">
          <div class="text-subtitle-1">Password</div>
          <v-text-field
            type="password"
            v-model="formData.password"
            @input="v$.password.$touch"
            @blur="v$.password.$touch"
            :error-messages="v$.password.$errors.map((e) => e.$message)"
            required
            density="compact"
            variant="outlined"
          ></v-text-field>
        </div>
        <div class="btn w-100 d-flex justify-center pa-3">
          <v-btn
            :disabled="disabled"
            id="v-btn"
            type="submit"
            class="v-btn v-btn--block rounded-lg elevation-0 pa-8 mt-10 rounded text-h6"
            >Login</v-btn
          >
        </div>
      </v-form>
    </div>
  </div>
</template>



<script setup>
import { ref, reactive, computed, watch } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, minLength } from "@vuelidate/validators";
import axios from "axios";

const endpoint = ref("https://tiny-blue-iguana-wig.cyclic.app");
const formData = reactive({
  username: "",
  password: "",
});

const rules = computed(() => ({
  username: {
    required,
  },
  password: {
    required,
    minLength: minLength(6),
  },
}));

// Watch for changes in the formData object
watch(
  formData,
  (newFormData, oldFormData) => {
    // Check if any of the formData fields have values
    const bothHaveValues =
      newFormData.username !== "" && newFormData.password !== "";

    // Update the disabled variable based on whether formData has values
    disabled.value = !bothHaveValues;
  },
  { deep: true }
);

const v$ = useVuelidate(rules, formData);

const disabled = ref(true);
// console.log($v.$validate);
const submit = async () => {
  const isFormCorrect = await v$.value.$validate();
  // Validate the form
  if (!isFormCorrect) {
    disabled.value = true;
    return;
  }

  // If form is valid, proceed with login
  loginUser();
};

const loginUser = async () => {
  try {
    const res = await axios.post(`${endpoint.value}/api/loginUser`, formData);

    if (res.status === 200) {
      console.log("login successful", res.data);
      window.location = "http://www.google.com";
    }
  } catch (err) {
    console.log("Failed to login user", err.message);
  }
};
</script>

<style>
.error {
  position: absolute;
  top: 7.8rem;
}

#v-btn {
  background-color: #b54e00;
  color: white;
}
/* .head {
  width: 100%;
} */
.head span {
  font-size: 6vw;
  font-weight: bold;
}

.form-group {
  width: 100%;
}

.signinText {
  color: black;
  border-bottom: 1px solid gray;
}

.signinText span {
  font-weight: bolder;
}

.text-subtitle-1 {
  color: black;
  font-weight: bolder;
}

#vsheet {
  border-top: 4px solid #fb730b;
}

@media screen and (min-width: 500px) {
  .head span {
    font-size: 1.4rem;
  }
}

@media screen and (min-width: 500px) {
  #form {
    width: 100%;
    display: flex;
  }
}
</style>
