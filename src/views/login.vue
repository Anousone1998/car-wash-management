<template>
 <v-app>
    <v-container fluid>
    <v-row align="center" justify="center" class="pt-15">
      <v-col md="10" cols="12">
        <v-card class="elevation-12">
          <v-row>
            <v-col cols="12" md="6" class="teal accent-2"></v-col>
            <v-col cols="12" md="6">
              <v-card-text class="mt-12">
                <h1 class="text-center">KP CARCARE</h1>
                <form class="ma-6" align="center" jutify="center" @submit.prevent="login">
                  <v-text-field
                    outlined
                    v-model="username"
                    :error-messages="nameErrors"
                    :counter="10"
                    label="Username"
                    required
                    @input="$v.name.$touch()"
                    @blur="$v.name.$touch()"
                  ></v-text-field>
                  <v-text-field
                    outlined
                    v-model="password"
                    :error-messages="emailErrors"
                    label="Password"
                    required
                    @input="$v.email.$touch()"
                    @blur="$v.email.$touch()"
                  ></v-text-field>
                  <v-btn
                    dark
                    width="100%"
                    depressed
                    color="teal accent-2"
                    @click="submit"
                    x-large
                    elevation="5"
                    type="submit"
                  >
                    LOGIN
                  </v-btn>
                </form>
              </v-card-text>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
 </v-app>
</template>

<script>
export default {
  data: () => ({
    username: "",
    password: "",
    user: "Lactasoiy",
    pass: "12345678",
  }),
  methods: {
    login() {
      if (this.username === this.user && this.password === this.pass) {
        localStorage.setItem("username", this.username);
        window.location = "Home.vue";
      } else {
        alert("Invalid username or password!");
      }
    },
  },
  name: "Login",
};
</script>
