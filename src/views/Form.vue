<template>
  <div>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <v-card class="elevation-12">
            <v-toolbar color="primary" dark flat>
              <v-toolbar-title>Login form</v-toolbar-title>
              <v-spacer />
            </v-toolbar>

            <v-card-text>
              <form>
                <v-text-field
                  v-model="name"
                  :error-messages="nameErrors"
                  label="name"
                  reqired
                  prepend-icon="mdi-account-circle"
                  @input="$v.name.$touch()"
                  @blur="$v.name.$touch()"
                />
                <v-text-field
                  id="surname"
                  label="surname"
                  name="surname"
                  prepend-icon="mdi-account-circle"
                  type="surname"
                  v-model="surname"
                  @input="$v.surname.$touch()"
                  @blur="$v.surname.$touch()"
                  :error-messages="surnameErrors"
                />
                <v-text-field
                  id="phone"
                  label="phone"
                  name="phone"
                  prepend-icon="mdi-cellphone-basic"
                  type="phone"
                  v-model="phone"
                  @input="$v.phone.$touch()"
                  @blur="$v.phone.$touch()"
                  :error-messages="phoneErrors"
                />
                <v-text-field
                  label="Email"
                  name="email"
                  prepend-icon="mdi-email"
                  type="email"
                  v-model="email"
                  @input="$v.email.$touch()"
                  @blur="$v.email.$touch()"
                  :error-messages="emailErrors"
                />
              </form>
            </v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn @click="submit" color="primary">Share</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, maxLength, email, numeric } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],

  validations: {
    name: { required, maxLength: maxLength(10) },
    surname: { required, maxLength: maxLength(10) },
    email: { required, email },
    phone: { required, numeric }
  },

  computed: {
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 10 characters long");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    surnameErrors() {
      const errors = [];
      if (!this.$v.surname.$dirty) return errors;
      !this.$v.surname.maxLength &&
        errors.push("Surname must be at most 10 characters long");
      !this.$v.surname.required && errors.push("Surname is required.");
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    },
    phoneErrors() {
      const errors = [];
      if (!this.$v.phone.$dirty) return errors;
      !this.$v.phone.numeric && errors.push("Must be numeric");
      !this.$v.phone.required && errors.push("Phone is required");
      return errors;
    },
    withNewUser() {
      const oldUsers = JSON.parse(localStorage.getItem("users"));
      const createdUser = {
        name: this.name,
        surname: this.surname,
        phone: this.phone,
        email: this.email
      };
      const newUsers = [...oldUsers, createdUser];
      return newUsers;
    },
    withUpdatedUser() {
      const oldUsers = JSON.parse(localStorage.getItem("users"));
      const createdUser = {
        name: this.name,
        surname: this.surname,
        phone: this.phone,
        email: this.email
      };
      const updatedUsers = oldUsers.map(user =>
        user.email === this.memoisedEmail ? createdUser : user
      );
      return updatedUsers;
    }
  },

  methods: {
    resetData() {
      this.name = "";
      this.surname = "";
      this.phone = "";
      this.email = "";
    },
    submit() {
      console.log("submit!");
      this.$v.$touch();
      if (this.$v.$invalid) {
        alert("Data is not valid");
      } else {
        this.isEdited
          ? localStorage.setItem("users", JSON.stringify(this.withUpdatedUser))
          : localStorage.setItem("users", JSON.stringify(this.withNewUser));
        this.$router.push("/");
      }
    }
  },

  data() {
    const userObj = JSON.parse(localStorage.getItem("user")) || {
      name: "",
      surname: "",
      phone: "",
      email: ""
    };
    return {
      name: userObj.name,
      surname: userObj.surname,
      phone: userObj.phone,
      email: userObj.email,
      isEdited: userObj.isEdited,
      memoisedEmail: userObj.email
    };
  }
};
</script>