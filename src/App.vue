<template>
  <v-app>
    <!-- drawer メニュー -->
    <v-navigation-drawer
      v-model="drawer"
      width="300"
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
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-vuetify</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              Getting Started
            </v-list-item-title>
          </v-list-item>
          <v-list-group no-action>
            <template v-slot:activator>
              <v-list-item-icon>
                <v-icon>mdi-cogs</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>Customization</v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item href="https://google.co.jp/">
              <v-list-item-content>
                <v-list-item-title>
                  Customization Sub
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-palette</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              Styles & animations
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-container>
    </v-navigation-drawer>

    <!-- ヘッダー メニュー -->
    <v-app-bar color="grey darken-1" dark clipped-left app>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Vuetify</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn text>Button</v-btn>
      </v-toolbar-items>
      <v-btn text x-small>Button</v-btn>
      <v-btn text>Button</v-btn>
      <v-btn outlined>Button</v-btn>
      <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn v-on="on" text>Support<v-icon>mdi-menu-down</v-icon></v-btn>
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
              <v-list-item-title>ログアウト</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-main>
      <hello-world />
    </v-main>

    <!-- フッター メニュー -->
    <v-footer color="grey darken-1" dark app>
      Vuetify
    </v-footer>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  components: {
    HelloWorld
  },
  data() {
    return {
      drawer: true
    }
  }
};
</script>
