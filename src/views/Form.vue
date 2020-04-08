<template>
  <div class="about">
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <v-card class="elevation-12">
            <v-toolbar color="primary" dark flat>
              <v-toolbar-title>Login form</v-toolbar-title>
              <v-spacer />
            </v-toolbar>

            <v-card-text>
              <v-form>
                <v-text-field
                  id="name"
                  label="name"
                  name="name"
                  prepend-icon="mdi-account-circle"
                  type="name"
                  v-model="fields.name"
                  :rules="[rules.required]"
                />
                <v-text-field
                  id="surname"
                  label="surname"
                  name="surname"
                  prepend-icon="mdi-account-circle"
                  type="surname"
                  v-model="fields.surname"
                  :rules="[rules.required]"
                />
                <v-text-field
                  id="phone"
                  label="phone"
                  name="phone"
                  prepend-icon="mdi-cellphone-basic"
                  type="phone"
                  v-model="fields.phone"
                  :rules="[rules.phoneValidation, rules.min, rules.required]"
                />
                <v-text-field
                  label="Email"
                  name="email"
                  prepend-icon="mdi-email"
                  type="email"
                  v-model="fields.email"
                  :rules="[rules.required, rules.emailValidation]"
                />
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn color="primary">Share</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fields: {
        name: "",
        surname: "",
        phone: "",
        email: ""
      },
      rules: {
        required: value => !!value || "required field",
        min: v => v.length >= 7 || "Min 7 characters",
        emailValidation: val =>
          /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(val)
            ? true
            : "wrong email",
        phoneValidation: val => (/\D/.test(val) ? "only digits alowed" : true)
      }
    };
  }
};
</script>