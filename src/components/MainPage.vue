<template>
  <v-container>
    <v-form @submit="submit" onSubmit="return false;">
      <vue-tel-input
        v-model="phoneNumber"
        label="Phone Number"
        required
        @onValidate="onValidate"
      ></vue-tel-input>

      <v-btn @click="submit" :disabled="!isValid">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </v-form>
  </v-container>
</template>

<script>
import Vue from "vue";
import VueTelInput from 'vue-tel-input'

Vue.use(VueTelInput)

export default {

  data: () => ({
    phoneNumber: "",
    isValid: false,
  }),

  methods: {
    submit() {
      var phoneNumber = this.phoneNumber.replace(new RegExp("\\+| ", 'g'), "");
      // console.log("bb", phoneNumber);
      window.location.href = "https://api.whatsapp.com/send?phone=" + phoneNumber;
    },
    clear() {
      this.phoneNumber = "";
    },
    onValidate({ number, isValid, country }) {
      this.isValid = isValid;
    }
  }
};
</script>

<style>
  @import "../../node_modules/vue-tel-input/dist/vue-tel-input.css"
</style>
