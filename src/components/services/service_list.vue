<template>
  <v-container>
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
   
  }),
};
</script>
