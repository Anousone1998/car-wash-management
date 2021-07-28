<template>
  <v-data-table :headers="headers" :items="products" class="elevation-1">
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>ສິນຄ້າທັງໝົດ</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="700px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
              ເພີ່ມສິນຄ້າ
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      v-model="editedItem.id"
                      outlined
                      label="ID"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      v-model="editedItem.bill_no"
                      label="ເລກບິນການສັ່ງຊື້"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      v-model="editedItem.product_name"
                      outlined
                      label="ຊື່ສິນຄ້າ"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-select
                      v-model="select"
                      :items="items"
                      outlined
                      label="ປະເພດສິນຄ້າ"
                      required
                    ></v-select>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      outlined
                      v-model="editedItem.qty"
                      label="ຈຳນວນ"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="gray darken-1" text @click="close">
                ຍົກເລີກ
              </v-btn>
              <v-btn color="blue darken-1" text @click="save">
                ບັນທຶກ
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5"
              >ທາ່ນຕ້ອງການລຶບຂໍ້ມູນນີ້ແທ້ບໍ່?</v-card-title
            >
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="gray darken-1" text @click="closeDelete"
                >ຍົກເລີກ</v-btn
              >
              <v-btn color="red darken-1" text @click="deleteItemConfirm"
                >ລຶບ</v-btn
              >
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:[`item.actions`]="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon small @click="deleteItem(item)">
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>
</template>

<script>
export default {
  name: "products",
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "ID",
        align: "start",
        sortable: false,
        value: "id",
      },
      { text: "ເລກທີບິນສັ່ງຊື້", value: "bill_no", sortable: false },
      { text: "ຊື່ສິນຄ້າ", value: "product_name", sortable: false },
      { text: "ປະເພດ", value: "type", sortable: false },
      { text: "ຈຳນວນ", value: "qty", sortable: false },
      { text: "ຈັດການ", value: "actions", sortable: false },
    ],
    products: [],
    editedIndex: -1,
    editedItem: {
      bill_no: "",
      product_name: "",
      type: "",
      qty: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "ເພີ່ມພະນັກງານໃໝ່" : "ແກ້ໄຂພະນັກງານ";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.products = [
        {
          id: "023",
          bill_no: "123",
          product_name: "spray",
          type: "jelly",
          qty: 2,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.products.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.products.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.products.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.products[this.editedIndex], this.editedItem);
      } else {
        this.products.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>
