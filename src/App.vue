<template>
  <v-app>
    <!-- drawer メニュー -->
    <v-navigation-drawer
      v-model="drawer"
      width="280"
      clipped
      app
    >
      <v-container>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title grey--text text--darken-2">
              Navigation Lists
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list nav>
          <v-list-group
              v-for="nav_list in nav_lists"
              :key="nav_list.name"
              :prepend-icon="nav_list.icon"
              no-action
              :append-icon="nav_list.lists ? undefined : ''">
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>{{ nav_list.name }}</v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item v-for="list in nav_list.lists" :key="list">
              <v-list-item-content>
                <v-list-item-title>{{ list }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
        </v-list>
      </v-container>
    </v-navigation-drawer>

    <!-- ヘッダー メニュー -->
    <v-app-bar color="grey darken-1" dark clipped-left app>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Vuetify UI Sample</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-text-field
        filled
        label="検索"
        autocomplete="off"
        class="rounded-lg mx-2 mx-md-4"
        clearable
        dense
        hide-details
        solo
        style="max-width: 450px;"
        background-color="grey"
      >
        <template #prepend-inner>
          <v-icon
            class="ml-1 mr-2"
          >
            mdi-magnify
          </v-icon>
        </template>
      </v-text-field>
      <v-toolbar-items>
        <v-btn text>Button</v-btn>
      </v-toolbar-items>
      <v-btn text x-small>Button</v-btn>
      <v-btn text>Button</v-btn>
      <v-btn outlined>Button</v-btn>
      <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn v-on="on" text>Menu<v-icon>mdi-menu-down</v-icon></v-btn>
        </template>
        <v-list>
          <v-subheader>Menu</v-subheader>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-vuetify</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Vuetify Menu</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-github</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Github Menu</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item href="https://google.co.jp/">
            <v-list-item-icon>
              <v-icon>mdi-logout</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>logout</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <!-- メインコンテンツ -->
    <v-main>
      <div class="my-5 ml-5">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              class="ma-2"
              color="primary"
              dark
              v-bind="attrs"
              v-on="on"
            >
              Tooltip
            </v-btn>
          </template>
          <span>Tooltip</span>
        </v-tooltip>
        <v-btn
          class="ma-2"
          :loading="loading"
          :disabled="loading"
          color="secondary"
          @click="loader = 'loading'"
        >
          Loader
        </v-btn>
        <v-btn
          class="ma-2"
          color="success"
        >
          Upload
          <v-icon
            right
            dark
          >
            mdi-cloud-upload
          </v-icon>
        </v-btn>
        <v-btn
          color="info"
          class="ma-2 white--text"
          fab
        >
          <v-icon dark>
            mdi-cloud-upload
          </v-icon>
        </v-btn>
      </div>
      <v-divider></v-divider>
      <v-subheader>Data Table Header</v-subheader>
      <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="10"
          class="elevation-1"
      ></v-data-table>
<!--      <hello-world />-->
    </v-main>

    <!-- フッター メニュー -->
    <v-footer color="grey darken-1" dark app>
      <v-container>
        <v-row justify="center">
          Vuetify UI Sample 2021 All rights reserved
        </v-row>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  components: {
    // HelloWorld
  },
  watch: {
    loader () {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 3000)

      this.loader = null
    },
  },
  data() {
    return {
      drawer: true,
      loader: null,
      loading: false,
      nav_lists:[
        {
          name: 'Getting Started',
          icon: 'mdi-speedometer',
          lists:['Quick Start','Pre-made layouts']
        },
        {
          name: 'Customization',
          icon: 'mdi-cogs'
        },
        {
          name: 'Styles & animations',
          icon: 'mdi-palette',
          lists:['Colors','Content','Display']
        },
        {
          name: 'UI Components',
          icon: 'mdi-view-dashboard',
          lists:['API explorer','Alerts']
        },
        {
          name: 'Directives',
          icon: 'mdi-function'
        },
        {
          name: 'Preminum themes',
          icon: 'mdi-vuetify'
        },
      ],
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Iron (%)', value: 'iron' },
      ],
      desserts: [
        { name: 'Frozen Yogurt', calories: 159, fat: 6.0, carbs: 24, protein: 4.0, iron: '1%', },
        { name: 'Ice cream sandwich', calories: 237, fat: 9.0, carbs: 37, protein: 4.3, iron: '1%', },
        { name: 'Eclair', calories: 262, fat: 16.0, carbs: 23, protein: 6.0, iron: '7%', },
        { name: 'Cupcake', calories: 305, fat: 3.7, carbs: 67, protein: 4.3, iron: '8%', },
        { name: 'Gingerbread', calories: 356, fat: 16.0, carbs: 49, protein: 3.9, iron: '16%', },
        { name: 'Jelly bean', calories: 375, fat: 0.0, carbs: 94, protein: 0.0, iron: '0%', },
        { name: 'Lollipop', calories: 392, fat: 0.2, carbs: 98, protein: 0, iron: '2%', },
        { name: 'Honeycomb', calories: 408, fat: 3.2, carbs: 87, protein: 6.5, iron: '45%', },
        { name: 'Donut', calories: 452, fat: 25.0, carbs: 51, protein: 4.9, iron: '22%', },
        { name: 'KitKat', calories: 518, fat: 26.0, carbs: 65, protein: 7, iron: '6%', },
      ],
    }
  }
};
</script>
