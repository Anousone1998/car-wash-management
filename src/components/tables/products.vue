<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="calories"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Products</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="700px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              ເພີ່ມ
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.product_id"
                      outlined
                      label="ລະຫັດສິນຄ້າ"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                    outlined
                      v-model="editedItem.bill_no"
                       label="ລະຫັດບິນ"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                    outlined
                      v-model="editedItem.name"
                      label="ຊື່ສິນຄ້າ"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                      v-model="editedItem.type"
                      outlined
                      label="ປະເພດສິນຄ້າ"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="6"
                  >
                    <v-text-field
                    outlined
                      v-model="editedItem.amount"
                      label="ຈຳນວນ"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
   <template v-slot:[`item.actions`]="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>

  </v-data-table>
</template>

<script>
  export default {
      name: 'products',
    data: () => ({
      dialog: false,
      dialogDelete: false,
      headers: [
        {
          text: 'ລະຫັດສິນຄ້າ',
          align: 'start',
          sortable: false,
          value: 'product_id',
        },
         { text: 'ລະຫັດບິນ', value: 'bill_no',sortable: false, },
        { text: 'ຊື່ສິນຄ້າ', value: 'name',sortable: false, },
        { text: 'ປະເພດສິນຄ້າ', value: 'type', sortable: false, },
        { text: 'ຈຳນວນ', value: 'amount', sortable: false, },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      products: [],
      editedIndex: -1,
      editedItem: {
        ລະຫັດສິນຄ້າ: '',
        ລະຫັດບິນ: '',
        ຊື່ສິນຄ້າ: '',
        ປະເພດສິນຄ້າ: '',
        ຈຳນວນ: '',
      },
      defaultItem: {
         ລະຫັດສິນຄ້າ: '',
        ລະຫັດບິນ: '',
        ຊື່ສິນຄ້າ: '',
        ປະເພດສິນຄ້າ: '',
        ຈຳນວນ: '',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'ເພີ່ມສິນຄ້າ' : 'ແກ້ໄຂ'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.products = [
          { 
            product_id: '23456',
            bill_no: '1234',
            name: 'Frome',
            type: spray,
            amount: 6,
          },
         {
            product_id: '23456',
            bill_no: '2310',
            name: 'Frome',
            type: 'jell',
            amount: 3,
          },
        ]
      },

      editItem (item) {
        this.editedIndex = this.products.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.products.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.products.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.products[this.editedIndex], this.editedItem)
        } else {
          this.products.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>