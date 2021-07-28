<template>
  <v-data-table
    :headers="headers"
    :items="supilers"
    sort-by="supiler_name"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>ຜູ້ສະໜອງ</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="700px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
              ເພີ່ມຜູ້ສະໜອງ
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
                      v-model="editedItem.supiler_id"
                      label="ID"
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field
                      v-model="editedItem.supiler_name"
                      label="ຊື່ຜູ້ສະໜອງ"
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
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="gray" text @click="close">
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
              <v-btn color="blue darken-1" text @click="deleteItemConfirm"
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
  name: "supiler",
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
      { text: "ຊື່ຜູ້ສະໜອງ", value: "supiler_name",sortable: false },
      { text: "ເບີໂທ", value: "phone",sortable: false },
      { text: "ທີ່ຢູ່", value: "address",sortable: false },
      { text: "ຈັດການ", value: "actions", sortable: false },
    ],
    supilers: [],
    editedIndex: -1,
    editedItem: {
      id: 0,
      supiler_name: '',
      phone: 0,
      address: '',
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "ເພີ່ມຜູ້ສະໜອງ" : "ແກ້ໄຂ";
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
      this.supilers = [
        {
          id: "123",
          supiler_name: "ວຽງລາຕີ",
          phone: '020 55696952',
          address: 'ໄຊຍະລີ'
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.supilers.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.supilers.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.supilers.splice(this.editedIndex, 1);
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
        Object.assign(this.supilers[this.editedIndex], this.editedItem);
      } else {
        this.supilers.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>
