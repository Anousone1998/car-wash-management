<template>
    <div>
      <h2 class="mt-3">Manage Products</h2>
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
         <report/>
      </v-card>
      </v-tab-item>
    </v-tabs-items>
    </div>
</template>

<script>
import report from '@/components/tables/report'
  export default {
    components: {
      report
    },
    data () {
      return {
        tab: null,
        items: [
          'passive income', 'Product Ordered'
        ],
       
      }
    },
  }
</script>

