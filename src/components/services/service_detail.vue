<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-row>
        <v-col cols="6" md="6">
          <h2>ລົດກຳລັງໃຊ້ບໍລິການ</h2>
        </v-col>
        <v-col cols="6" md="6" class="d-flex justify-end ">
          <v-btn dark color="cyan" v-bind="attrs" v-on="on"
            ><v-icon>mdi-plus</v-icon>ເພີ່ມລົດໃໝ່</v-btn
          >
        </v-col>
      </v-row>
      <v-row>
       <v-col cols="12" md="12" sm="12">
          <v-card class="mt-3" v-for="(item, index) in newItems" :key="index">
          <v-card-text>
            <v-row>
              <v-col md="3"
                ><span>
                  <strong> ທະບຽນລົດ:</strong> {{ item.car_id }}
                </span></v-col
              >
              <v-col md="6"
                ><span
                  ><strong>ປະເພດລົດ: </strong>{{ item.car_type[index] }}</span
                ></v-col
              >
              <v-col md="3" class="d-flex justify-end "
                ><span
                  ><strong>ຊື່ລູກຄ້າ: </strong
                  >{{ item.customer_name }}</span
                ></v-col
              >
            </v-row>
            <v-divider></v-divider>
            <br />
            <v-row class="ml-1 mr-1">
              <p>ລາຍການບໍລິການ</p>
              <v-spacer></v-spacer>
              <v-btn outlined color="primary" dark v-bind="attrs" v-on="on"
                >edit</v-btn
              >
            </v-row>

            <!-- service detail -->
            <v-col cols="12" md="12" class="d-flex flex-row ">
              <v-card outlined width="100" height="100" class="pt-2 mr-2">
                <v-card-text>
                  <v-row justify="center" align="center">
                    <span>{{ item.service}}</span>
                  </v-row>
                  <v-row justify="center" align="center">
                    <!-- <v-icon large>{{item.service.icon}}</v-icon> -->
                  </v-row>
                  <v-row justify="center" align="center">
                    <span><strong>{{item.price}}</strong></span>
                  </v-row>
                </v-card-text>
              </v-card>
            </v-col>
          </v-card-text>
          <v-card-actions class="pt-0">
            <v-row>
              <v-col md="10" sm="10" class="d-flex justify-end mb-2 ">
                <span><strong>sub total:</strong> 359,000 k</span>
              </v-col>
              <v-col md="2" sm="2" class="d-flex justify-end ">
                <bill />
              </v-col>
            </v-row>
          </v-card-actions>
        </v-card>
       </v-col>
      </v-row>
    </template>

    <!-- add customer -->
    <v-card>
      <v-card-title>
        <span class="text-h5">ເພີ່ມຂໍ້ມູນລູກຄ້າ</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="6">
              <v-text-field
                v-model="item.customer_name"
                type="text"
                label="ຊື່ລູກຄ້າ"
                outlined
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="6">
              <v-text-field 
              outlined 
   v-model="item.phone"
              label="ເບີໂທ"></v-text-field>
            </v-col>
            <v-col cols="12" md="6" sm="6">
              <v-text-field
                label="ເລກທະບຽນລົດ"
                outlined
                v-model="item.car_id"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="6">
              <v-select
                v-model="car_type"
                :items="item.car_type"
                label="ປະເພດລົດ"
                outlined
                required
              ></v-select>
            </v-col>

            <v-col cols="12" sm="6" md="6">
              <v-select
                v-model="car_brand"
                :items="item.car_brand"
                label="ຍີ່ຫໍ້ລົດ"
                outlined
              ></v-select>
            </v-col>

            <v-col cols="12" md="12">
              <span>ເລືອກບໍລິການ</span><br />
              <v-row>
                <v-checkbox class="ml-2" v-model="service" label="ລ້າງນອກ" value="serivce1"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ລ້າງລົດ" value="service2"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ປ່ຽນນ້ຳມັນເຄື່ອງ" value="service3"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ເຕີມນ້ຳຢາຫມໍ້ນ້ຳ" value="service4"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ຂັດສີ-ເຄືອບເງົາ" value="service5"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ເຄືອບເງົາ" value="service6"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ຂັດເບາະ" value="service7"></v-checkbox>
                 <v-checkbox class="ml-2" v-model="service" label="ຂັດຢາງໝາກຕອຍ" value="service8"></v-checkbox>
              </v-row>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="gray" text @click="dialog = false">
          Cancel
        </v-btn>
        <v-btn color="blue darken-1" text @click="addItem">
          Submit
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import bill from "@/components/bill_pay/bill.vue";
export default {
  methods: {
    addItem() {
      this.newItems.push(this.item), (this.dialog = false);
      this.item = { car_id: "", car_type: "",car_brand: "", customer_name: "", price: "", phone: ""};
    },
  },
  name: "service_detail",
  components: {
    bill,
  },

  data: () => ({
   
    // items: ["Item 1", "Item 2", "Item 3", "Item 4"],

    dialog: false,
    item: {
       select_type: null,
       select_bra: null,
      phone: '',
      car_type: ["SUV", "Pick"],
      car_brand: ["TOYOTA", "HONDA"],
      car_id: "",
      customer_name: "",
       price: "35,000"
    },
    newItems: [],
  }),
};
</script>
