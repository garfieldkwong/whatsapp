<template>
  <v-container>
    <v-form @submit="submit" onSubmit="return false;">
      <v-text-field
        v-validate="'required|decimal'"
        v-model="phoneNumber"
        :error-messages="errors.collect('phoneNumber')"
        label="Phone Number"
        data-vv-name="phoneNumber"
        required
      ></v-text-field>

      <v-btn @click="submit">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </v-form>
  </v-container>
</template>

<script>
import Vue from "vue";
//   import VueTelInput from 'vue-tel-input'
import VeeValidate from "vee-validate";

//   Vue.use(VueTelInput)
Vue.use(VeeValidate);

export default {
  $_veeValidate: {
    validator: "new"
  },

  data: () => ({
    phoneNumber: ""
  }),

  methods: {
    submit() {
      this.$validator.validateAll().then(result => {
        if (result) {
          window.location.href =
            "https://api.whatsapp.com/send?phone=" + this.phoneNumber;
        }
      });
    },
    clear() {
      this.phoneNumber = "";
      this.$validator.reset();
    }
  }
};
</script>

<style>
</style>
