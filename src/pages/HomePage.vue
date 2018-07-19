<template>
  <v-ons-page>
    <v-ons-toolbar class="home-toolbar">
      <div class="left">
        <v-ons-toolbar-button @click="$store.commit('splitter/toggle')">
          <v-ons-icon icon="fa-bars"></v-ons-icon>
        </v-ons-toolbar-button>
      </div>
      <div class="center">{{ msg }}</div>
    </v-ons-toolbar>

    <div class="header">
      <img src="../assets/logo.png" alt="vue-logo">
    </div>

    <p align="center">{{ weather_time }} : {{ weather }}</p>
    <v-ons-button modifier="large" @click="$router.push({name:'hoge-page'});">
      Hoge!
    </v-ons-button>
    <v-ons-list-title>Vue.js Essential Links</v-ons-list-title>
    <v-ons-list>
      <v-ons-list-item v-for="item in essentialLinks" @click="goTo(item.link)" :key="item.link">
        <div class="left"><v-ons-icon fixed-width :icon="item.icon"></v-ons-icon></div>
        <div class="center">{{ item.label }}</div>
        <div class="right"><v-ons-icon icon="fa-external-link"></v-ons-icon></div>
      </v-ons-list-item>
    </v-ons-list>

    <v-ons-list-title>Vue.js Essential Links</v-ons-list-title>
    <v-ons-row>
      <v-ons-col>
        <v-ons-card @click="goTo('http://router.vuejs.org/')">vue-router</v-ons-card>
      </v-ons-col>
      <v-ons-col>
        <v-ons-card @click="goTo('http://vuex.vuejs.org/')">vuex</v-ons-card>
      </v-ons-col>
    </v-ons-row>
    <v-ons-row>
      <v-ons-col>
        <v-ons-card @click="goTo('http://vue-loader.vuejs.org/')">vue-loader</v-ons-card>
      </v-ons-col>
      <v-ons-col>
        <v-ons-card @click="goTo('https://github.com/vuejs/awesome-vue')">awesome-vue</v-ons-card>
      </v-ons-col>
    </v-ons-row>

  </v-ons-page>
</template>

<script>
export default {
  name: 'home-page',
  data () {
    return {
      api_url: 'http://api.openweathermap.org/data/2.5/forecast?q=kagoshima-shi,jp&APPID=',
      api_key: '', // My API Key
      msg: 'welcome',
      weather_time: '',
      weather: '',
      essentialLinks: [
        {
          label: 'Core Docs',
          link: 'https://vuejs.org',
          icon: 'fa-book'
        },
        {
          label: 'Community Chat',
          link: 'https://chat.vuejs.org',
          icon: 'fa-commenting'
        },
        {
          label: 'Forum',
          link: 'https://forum.vuejs.org',
          icon: 'fa-comments'
        },
        {
          label: 'Twitter',
          link: 'https://twitter.com/vuejs',
          icon: 'fa-twitter'
        },
        {
          label: 'Docs for this template',
          link: 'http://vuejs-templates.github.io/webpack/',
          icon: 'fa-file-text'
        }
      ]
    }
  },
  methods: {
    goTo (url) {
      const newWindow = window.open(url, '_blank')
      newWindow.opener = null
      newWindow.location = url
    }
  },
  computed: {
    geturl: function () {
      return this.api_url + this.api_key
    }
  },
  mounted () {
    this.axios
      .get(this.geturl)
      .then((res) => {
        this.weather = res.data.list[0].weather[0].description
        this.weather_time = res.data.list[0].dt_txt
      })
      .catch((res) => {
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  text-align: center;
}

img {
  max-width: 300px;
}

ons-list-title {
  text-transform: none;
}

ons-list-title:not(:first-of-type) {
  margin-top: 30px;
}

ons-card {
  text-align: center;
}

ons-list-item, ons-card {
  cursor: pointer;
}
</style>
