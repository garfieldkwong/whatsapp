<template>
  <v-container>
    <v-form @submit="submit" onSubmit="return false;">
      <vue-tel-input
        v-model="phoneNumber"
        label="Phone Number"
        required
        @onValidate="onValidate"
        @onInput="onInput"
      ></vue-tel-input>
      <v-alert
        :value="showAlert"
        type="error"
      >Please input a valid phone number</v-alert>

      <v-btn @click="submit" :disabled="!isValid">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </v-form>
  </v-container>
</template>

<script>
import Vue from "vue";
import VueTelInput from "vue-tel-input";

Vue.use(VueTelInput);

export default {
  data: () => ({
    phoneNumber: "",
    isValid: false,
    showAlert: false,
    timeoutID: null,
  }),

  methods: {
    submit() {
      var phoneNumber = this.phoneNumber.replace(new RegExp("\\+| ", "g"), "");
      window.location.href =
        "https://api.whatsapp.com/send?phone=" + phoneNumber;
    },
    clearTimer() {
      if (this.timeoutID !== null) {
        clearTimeout(this.timeoutID);
        this.timeoutID = null;
      }
    },
    clear() {
      this.phoneNumber = "";
      this.showAlert = false;
      this.isValid = false;
      this.clearTimer();
    },
    onValidate({ number, isValid, country }) {
      this.isValid = isValid;
    },
    onInput({ number, isValid, country }) {
      this.showAlert = false;
      this.clearTimer();
      if (!isValid && !(number === "")) {
        var self = this;
        this.timeoutID = setTimeout(
          function() {
            self.showAlert = true;
          }, 1000
        );
      }
    }
  }
};
</script>

<style>
@import "../../node_modules/vue-tel-input/dist/vue-tel-input.css";
</style>
