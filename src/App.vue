<template>
  <v-app style="background: #1F2128">
    <v-navigation-drawer app permanent width="360">
      <tutorial-card :guide="guide" :currentGuideItem="currentGuideItem"/>
    </v-navigation-drawer>
    <v-main>
      <v-container
        style="display: flex; justify-content: center; align-items: center; height:50%"
      >
        <v-card rounded="lg" flat style="background: #242731" width="600">
          <v-card-text>
            <v-card-title>
              <v-icon left large color="accent">mdi-bank</v-icon>Big Corpo Bank
            </v-card-title>
            <v-card-subtitle>
              Trust <strong>us</strong> with <u>your</u> money
              <v-icon style="color: inherit">mdi-currency-usd</v-icon> ;)
            </v-card-subtitle>
          </v-card-text>
          <v-card-text>
            <v-form @submit.prevent="attemptLogin" id="login-form">
              <v-text-field required v-model="email" type="email" outlined rounded label="E-Mail" />
              <v-text-field required v-model="password" type="password" outlined rounded label="Password" :hint="password" />
              <v-card-actions style="display: flex">
                <v-hover v-slot="{ hover }" v-if="false">
                  <v-btn
                    rounded
                    depressed
                    :x-large="hover"
                    :fab="!hover"
                    :style="`height: 52px; width: ${hover ? 'auto' : '52px'};`"
                    :ripple="false"
                    class="secondary darken-1"
                  >
                    <v-icon color="grey">mdi-wallet-plus-outline</v-icon
                    ><v-fade-transition hide-on-leave
                      ><span class="grey--text" v-if="hover"
                        >Register</span
                      ></v-fade-transition
                    >
                  </v-btn>
                </v-hover>
                <v-btn style="flex: 1" rounded depressed x-large color="accent" type="submit" form="login-form">
                  <v-icon>mdi-wallet-outline</v-icon>Sign In
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card-text>
        </v-card>
      </v-container>
      <v-container
        style="display: flex; justify-content: space-around; align-items: center; height:50%"
      >
        <log-window/>
        <code-snippet :email="email" :password="password"/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import CodeSnippet from './components/CodeSnippet.vue';
import LogWindow from './components/LogWindow.vue';
import TutorialCard from './components/TutorialCard.vue';
export default {
  name: 'App',

  components: {CodeSnippet, LogWindow, TutorialCard},

  data: () => ({
    email: '',
    password: '',
    
    currentGuideItem: 0,
    guide: [
      {
        title: 'Einführung',
        instructions: 'Tue dies und das um das zu machen, damit es dies und das tun kann',
      },
      {
        title: 'Einführung',
        instructions: 'Tue dies und das um das zu machen, damit es dies und das tun kann',
      },
    ],
  }),

  methods: {
    attemptLogin: async function (e){
      console.log(e)
      this.currentGuideItem ++;
    }
  }
};
</script>

<style>
html {
  overflow-y: hidden !important;
}
</style>
