<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title class="text-h6 purple--text text--darken-2">
          Todo App
        </v-list-item-title>
        <v-list-item-subtitle>
          Best todo in the market
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-divider></v-divider>

    <v-list
      dense
      nav
    >
      <v-list-item
        v-for="item in items"
        :key="item.title"
        :to="item.to"
        :class="{'purple lighten-2 white--text' : navTodo === item.title}"
        @click="setNavTodo(item.title)"
        v-model="navTodo"
        link
      >
        <v-list-item-icon>
          <v-icon>{{ item.icon }}</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
    </v-navigation-drawer>

    <v-app-bar app  
    color="#7B1FA2"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" color="white"></v-app-bar-nav-icon>

      <v-toolbar-title class="text-h6 white--text text--darken-2">Todo App</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn color="white" icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn color="white" icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn color="white" icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>

    </v-app-bar>

    <v-main>
      <!--  -->
      <v-container fluid>

        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
  
    </v-main>
  </v-app>
</template>

<script>
  export default {
    name: 'App',
    data: () => ({ drawer: null,items: [
          { title: 'Todo', icon: 'mdi-format-list-checks', to: '/', selected: true},
          { title: 'About', icon: 'mdi-help-box', to: '/about', selected: false },
        ],
        navTodo : sessionStorage.getItem('active') || 'Todo'
      }),
      methods: {
        setNavTodo(item){
          this.navTodo = item
          sessionStorage.setItem('active', this.navTodo)
        }
      }
  }
</script>