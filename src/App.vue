<template>
  <v-app>
    <!-- Navbar -->
    <v-navigation-drawer app dense color="#6CC9DF" dark>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            Car-wash
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav >
        <v-list-item v-for="item in items" :key="item.title" link @click="$router.push({ path: item.route })" >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- appbar -->
    <v-app-bar app dense >
      <div class="d-flex align-center"></div>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Car Wash</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text>
        <span class="mr-2">Username</span>
        <v-icon>mdi-account</v-icon>
      </v-btn>
    </v-app-bar>
    <!-- Content -->
    <v-main>
      <v-container fluid>
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    items: [
      {
           title: "ໜ້າຫຼັກ",
            icon: "mdi-car-cog",
            route: '/'
         },
      { 
          title: "Products",
           icon: "mdi-apps",
            route: '/manage_product'
         },
      {
           title: "Supilers",
            icon: "mdi-table-arrow-left",
            route: '/supilers'
     },
      {
           title: "Employees",
            icon: "mdi-account-group",
            route: '/employees'
     },
      {
           title: "Report",
            icon: " mdi-file-chart",
             route: '/report'
     },
      {
           title: "Manage Service",
            icon: "mdi-playlist-star"
     },
    ],
    right: null,
    //
  }),
};
</script>
