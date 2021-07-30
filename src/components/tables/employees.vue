<template>
  <v-data-table :headers="headers" :items="employees" class="elevation-1">
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>ພະນັກງານທັງໝົດ</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="700px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
              ເພີ່ມພະນັກງານໃໝ່
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
                      v-model="editedItem.emp_name"
                      label="ຊື່"
                      outlined
                    ></v-text-field>
                  </v-col>
                     <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      v-model="editedItem.emp_name"
                      label="ວັນເດືອນປີເກີດ"
                      outlined
                    ></v-text-field>
                  </v-col>
                
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      outlined
                      v-model="editedItem.phone"
                      label="ເບີໂທ"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      outlined
                      v-model="editedItem.address"
                      label="ທີ່ຢູ່"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      outlined
                      v-model="editedItem.start_date"
                      label="ມື້ເຂົ້າເຮັດວຽກ"
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
              <v-btn color="gray" text @click="closeDelete"
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
  name: "employees",
  data: () => ({
     activePicker: null,
      date: null,
      menu: false,
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "ID",
        align: "start",
        sortable: false,
        value: "id",
      },
      { text: "ຊື່ພະນັກງານ", value: "emp_name", sortable: false },
      { text: "ວັນເດືອນປີເກີດ", value: "dateOfBirth", sortable: false },
      { text: "ເບີໂທ", value: "phone", sortable: false },
      { text: "ທີ່ຢູ່", value: "address", sortable: false },
      { text: "ວັນ-ເວວລາເລີ່ມເຮັດວຽກ", value: "start_date" },
      { text: "ຈັດການ", value: "actions", sortable: false },
    ],
    employees: [],
    editedIndex: -1,
    editedItem: {
      emp_name: "",
      dateOfBirth: "",
      phone: "",
      address: "",
      start_date: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "ເພີ່ມພະນັກງານໃໝ່" : "ແກ້ໄຂພະນັກງານ";
    },
  },
  created() {
    this.initialize();
  },

  methods: {
   
    editItem(item) {
      this.editedIndex = this.employees.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.employees.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.employees.splice(this.editedIndex, 1);
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
        Object.assign(this.employees[this.editedIndex], this.editedItem);
      } else {
        this.employees.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>
