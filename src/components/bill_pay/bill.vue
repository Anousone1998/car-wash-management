<template>
  <v-row justify="center">
    <v-btn
      color="primary"
      dark
      @click.stop="dialog = true"
    >
      ຊຳລະຄ່າບໍລິການ
    </v-btn>

    <v-dialog
      v-model="dialog"
      max-width="500"
    >
      <v-card>
        <v-card-title class="text-h5">
         ການຊຳລະຄ່າບໍລິການ
        </v-card-title>

        <v-card-text>
            <v-row class="mt-5">
              <ul>
                <li><p>ໃບບິນເລກທີ: </p></li>
                 <li><p>ເວລາ ແລະ ວັນທີ: </p></li>
                  <li><p>ຊື່ລູກຄ້າ: </p></li>
                   <li><p>ເບີໂທ: </p></li>
                    <li><p>ທະບຽນລົດ: </p></li>
                     <li><p>ປະເພດລົດ: </p></li>
                    <v-divider></v-divider>
              </ul>
            </v-row>
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            color="gray1"
            text
            @click="dialog = false"
          >
            ຍົກເລີກ
          </v-btn>

          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
           ຊຳລະ
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  export default {
      name: 'bill',
    data () {
      return {
        dialog: false,
      }
    },
  }
</script>