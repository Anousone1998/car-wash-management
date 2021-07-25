<template>
  <v-container>
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-row>
          <v-col cols="6" md="6">
            <h2>car on servicing</h2>
          </v-col>
          <v-col cols="6" md="6" class="d-flex justify-end ">
            <v-btn dark color="cyan" v-bind="attrs" v-on="on"
              ><v-icon>mdi-plus</v-icon>Add car</v-btn
            >
          </v-col>
        </v-row>
        <!-- <v-btn

        >
          Open Dialog
        </v-btn> -->
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">Add New Customer</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="6">
                <v-text-field
                  label="Customer Name"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-text-field label="Phone" outlined></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-text-field label="Car ID" outlined required></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-select
                  :items="['0-17', '18-29', '30-54', '54+']"
                  label="Car Type"
                  outlined
                  required
                ></v-select>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-autocomplete
                  :items="[
                    'Skiing',
                    'Ice hockey',
                    'Soccer',
                    'Basketball',
                    'Hockey',
                    'Reading',
                    'Writing',
                    'Coding',
                    'Basejump',
                  ]"
                  label="Car brand"
                  outlined
                ></v-autocomplete>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="gray" text @click="dialog = false">
            Cancel
          </v-btn>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Submit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <service_detail />
  </v-container>
</template>

<script>
import service_detail from "@/components/services/service_detail";
export default {
  name: "service_list",

  components: {
    service_detail,
  },

  data: () => ({
    dialog: false,
  }),
};
</script>
