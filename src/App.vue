<template>
  <div id="app">
    <v-app id="inspire">
      <v-navigation-drawer fixed :clipped="$vuetify.breakpoint.lgAndUp" app v-model="drawer">
        <v-list dense>
          <template v-for="item in items">
            <v-layout row v-if="item.heading" align-center :key="item.heading">
              <v-flex xs6>
                <v-subheader v-if="item.heading">
                  {{ item.heading }}
                </v-subheader>
              </v-flex>
              <v-flex xs6 class="text-xs-center">
                <a href="#!" class="body-2 black--text">EDIT</a>
              </v-flex>
            </v-layout>
            <v-list-group v-else-if="item.children" v-model="item.model" :key="item.text" :prepend-icon="item.model ? item.icon : item['icon-alt']" append-icon="">
              <v-list-tile slot="activator">
                <v-list-tile-content>
                  <v-list-tile-title>
                    {{ item.text }}
                  </v-list-tile-title>
                </v-list-tile-content>
                <!--  -->
              </v-list-tile>
              <!-- list nhóm liên hệ -->
              <v-list-tile v-for="(child, i) in item.children" :key="i">
                <v-list-tile-action v-if="child.icon">
                  <v-btn icon flat @click="goGroup(child.value)">
                    <v-icon color="grey lighten-1">{{ child.icon }}</v-icon>
                  </v-btn>
                </v-list-tile-action>
                <!-- Đây là nhóm liên hệ -->
                <v-list-tile-content>
                  <v-list-tile-title>
                    {{child.text}}
                  </v-list-tile-title>
                </v-list-tile-content>
                <v-list-tile-action>
                  <v-list-tile-title>
                    <v-icon @click="editGroup(i)">mode_edit</v-icon>
                    <v-icon @click="delGroup(i)">delete</v-icon>
                  </v-list-tile-title>
                </v-list-tile-action>
                <!-- Nhóm liên hệ -->
              </v-list-tile>
              <!-- kết thúc list nhóm liên hệ -->
              <v-list-tile flat @click.native.stop="dialog = true">
                <v-list-tile-action>
                  <v-icon>add</v-icon>
                </v-list-tile-action>
                <!-- Đây là nhóm liên hệ -->
                <v-list-tile-content>
                  <v-list-tile-title>
                    Tạo nhóm liên hệ
                  </v-list-tile-title>
                </v-list-tile-content>

                <!-- Nhóm liên hệ -->
              </v-list-tile>

            </v-list-group>
            <!-- Đây là menu -->
            <v-list-tile v-else :key="item.text" flat :to="item.link">
              <v-list-tile-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ item.text }}
                </v-list-tile-title>
              </v-list-tile-content>
              <!--  -->
            </v-list-tile>
          </template>
        </v-list>
      </v-navigation-drawer>
      <v-toolbar color="blue darken-3" dark app :clipped-left="$vuetify.breakpoint.lgAndUp" fixed>
        <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
          <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
          <span class="hidden-sm-and-down">Google Danh bạ</span>
        </v-toolbar-title>

        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon>apps</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>notifications</v-icon>
        </v-btn>
        <v-btn icon large>
          <v-avatar size="32px" tile>
            <img src="https://vuetifyjs.com/static/doc-images/logo.svg" alt="Vuetify">
          </v-avatar>
        </v-btn>
      </v-toolbar>
      <v-content class="color-bg">
        <v-container fluid>
          <router-view />
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    drawer: null,
    items: [
      { icon: "contacts", text: "Danh bạ", link: "/" },
      {
        icon: "history",
        text: "Liên hệ thường xuyên",
        link: "/frequently-contacted"
      },
      { icon: "content_copy", text: "Nhóm", link: "/group" },
      {
        icon: "keyboard_arrow_up",
        "icon-alt": "keyboard_arrow_down",
        text: "Nhóm liên hệ",
        model: true,
        children: []
      },
      {
        icon: "keyboard_arrow_up",
        "icon-alt": "keyboard_arrow_down",
        text: "More",
        model: false,
        children: [
          { text: "Import" },
          { text: "Export" },
          { text: "Print" },
          { text: "Undo changes" },
          { text: "Other contacts" }
        ]
      },
      { icon: "settings", text: "Settings" },
      { icon: "chat_bubble", text: "Send feedback" },
      { icon: "help", text: "Help" },
      { icon: "phonelink", text: "App downloads" },
      { icon: "keyboard", text: "Go to the old version" }
    ],
    text: null,
    dialog: false
  })
};
</script>

<style>
.color-bg {
  background-color: white !important;
}
</style>
