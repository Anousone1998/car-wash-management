<template>
    <div>
      <h2 class="mt-3">ຈັດການຂໍ້ມູນບໍລິການ</h2>
   <v-row>
     <v-col md="6">
        <v-tabs
    class="mt-3"
      v-model="tab"
      background-color="transparent"
      color="basil"
    >
      <v-tab
        v-for="item in items"
        :key="item"
      >
        {{ item }}
      </v-tab>
    </v-tabs>
     </v-col>
   </v-row>
    <v-tabs-items v-model="tab">
      <v-tab-item
        v-for="item in items"
        :key="item"
      >
      <v-card class="pa-2">
         <service_management/>
      </v-card>
      </v-tab-item>
    </v-tabs-items>
    </div>
</template>

<script>
import service_management from '@/components/tables/service_management'
  export default {
    name: 'service_magement',
    components: {
      service_management
    },
    data () {
      return {
        tab: null,
        items: [
          'ລົດຈັກ', 'ລົດເກັງ', 'ລົດຕູ້', "ລົດຈິບ", "ລົດກະບະ"
        ],
       
      }
    },
  }
</script>

