<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col md="10" cols="12">
        <v-card class="elevation-12">
          <v-window v-model="step">
            <v-window-item :value="1">
              <v-row>
                 <v-col cols="12" md="6" class="teal accent-2"></v-col>
                <v-col cols="12" md="6">
                  <v-card-text class="mt-12">
                    <h1 class="text-center">KP CARCARE</h1>
                    <form class="ma-6" align="center" jutify="center">
                      <v-text-field
                        outlined
                        v-model="name"
                        :error-messages="nameErrors"
                        :counter="10"
                        label="Username"
                        required
                        @input="$v.name.$touch()"
                        @blur="$v.name.$touch()"
                      ></v-text-field>
                      <v-text-field
                        outlined
                        v-model="email"
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
                      >
                        LOGIN
                      </v-btn>
                    </form>
                  </v-card-text>
                </v-col>
               
              </v-row>
            </v-window-item>
          </v-window>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    step: 1,
  }),
  props: {
    source: String,
  },
  name: "Login",
};
</script>
