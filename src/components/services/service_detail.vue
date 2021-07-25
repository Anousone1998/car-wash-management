<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-card class="mt-3">
        <v-card-text>
          <v-row>
            <v-col md="3"
              ><span> <strong> Car ID:</strong> KB 1234 </span></v-col
            >
            <v-col md="6"
              ><span><strong>Car type</strong>: keng</span></v-col
            >
            <v-col md="3" class="d-flex justify-end "
              ><span><strong>Customer Name:</strong> justin</span></v-col
            >
          </v-row>
          <v-divider></v-divider>
          <br />
          <v-row class="ml-1 mr-1">
            <p>services</p>
            <v-spacer></v-spacer>
            <v-btn outlined color="primary" dark v-bind="attrs" v-on="on"
              >edit</v-btn
            >
          </v-row>
          <v-col cols="12" md="12" class="d-flex flex-row ">
            <v-card outlined width="100" height="100" class="pt-2 mr-2">
              <v-card-text>
                <v-row justify="center" align="center">
                  <span>Wash</span>
                </v-row>
                <v-row justify="center" align="center">
                  <v-icon large>mdi-car-settings</v-icon>
                </v-row>
                <v-row justify="center" align="center">
                  <span><strong>35,000 k</strong></span>
                </v-row>
              </v-card-text>
            </v-card>
            <v-card outlined width="100" height="100" class="pt-4 mr-2">
              <v-card-text>
                <v-row justify="center" align="center">
                  <span>Wash</span>
                </v-row>
                <v-row justify="center" align="center">
                  <span><strong>35,000 k</strong></span>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
        </v-card-text>
        <v-card-actions class="pt-0">
          <v-row>
            <v-col md="10" class="d-flex justify-end mb-2 ">
              <span><strong>sub total:</strong> 359,000 k</span>
            </v-col>
            <v-col md="2" class="d-flex justify-end ">
              <bill />
            </v-col>
          </v-row>
        </v-card-actions>
      </v-card>
    </template>
    <v-card>
      <v-card-title>
        <span class="text-h5">Edit Customer Services</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="6">
              <v-text-field label="Customer Name" outlined required></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="6">
              <v-text-field
              outlined
                label="Phone"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="6" sm="6">
              <v-text-field label="Car ID" 
              outlined
              required></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="6">
              <v-select
                :items="['0-17', '18-29', '30-54', '54+']"
                label="Car Type"
                required
                outlined
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
                label="Car Brand"
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
</template>

<script>
import bill from "@/components/bill_pay/bill.vue";
export default {
  name: "service_detail",
  components: {
    bill,
  },

  data: () => ({
    dialog: false,
  }),
};
</script>
