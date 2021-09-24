<template>
  <v-app style="background: #1F2128">
    <v-navigation-drawer app permanent width="360">
      <tutorial-card :guide="guide" :currentGuideItem="currentGuideItem" />
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
          <v-card-text v-if="!atEnd">
            <v-form @submit.prevent="attemptLogin" id="login-form">
              <v-text-field
                required
                v-model="email"
                type="email"
                outlined
                rounded
                label="E-Mail"
              />
              <v-text-field
                required
                v-model="password"
                type="password"
                outlined
                rounded
                label="Password"
                :hint="password"
              />
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
                <v-btn
                  style="flex: 1"
                  rounded
                  depressed
                  x-large
                  color="accent"
                  type="submit"
                  form="login-form"
                  :loading="loading"
                >
                  <v-icon>mdi-wallet-outline</v-icon>Sign In
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card-text>
          <v-card-text v-else>
            //addProfile
            <v-row>
              <v-col>
                <v-card-title class="pa-0 primary--text text--lighten-2">
                  Account
                </v-card-title>
              </v-col>
              <v-col>
                <v-card-title class="pa-0 font-weight-light">
                  Available Balance
                </v-card-title>
              </v-col>
              <v-col>
                <v-card-title class="pa-0 font-weight-light">
                  Present Balance
                </v-card-title>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-card-subtitle class="pa-0 font-weight-bold primary--text text--lighten-1">
                  Checking
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2">mdi-currency-usd</v-icon>5,200.23
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2">mdi-currency-usd</v-icon>5,200.23
                </v-card-subtitle>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-card-subtitle class="pa-0 font-weight-bold primary--text text--lighten-1">
                  Savings
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2">mdi-currency-usd</v-icon>70,213.65
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2">mdi-currency-usd</v-icon>70,213.65
                </v-card-subtitle>
              </v-col>
            </v-row>
          </v-card-text>
        </v-card>
      </v-container>
      <v-container
        style="display: flex; justify-content: space-around; align-items: center; height:50%"
      >
        <v-slide-y-transition
          group
          style="display: flex; justify-content: space-around; align-items: center; width: 100%"
        >
          <log-window key="logs" ref="logWindow" />
          <code-snippet
            key="code"
            :email="email"
            :password="password"
            v-if="currentGuideItem >= 2"
          />
        </v-slide-y-transition>
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

  components: { CodeSnippet, LogWindow, TutorialCard },

  data() {
    return {
      email: '',
      password: '',
      loading: false,

      currentGuideItem: 0,
      guide: [
        {
          title: 'Einführung',
          instructions: `
          <span>Geben Sie ein: 
            <div class="pt-1">
              E-Mail: <span class="primary--text text--lighten-2 font-weight-bold">test@email.com</span>
              <br/>
              Password: <span class="primary--text text--lighten-2 font-weight-bold">securePassword</span>
            </div>
            <div class="pt-1">
              Und schauen sie in die <strong class="primary--text text--lighten-1">Logs</strong>
            </div>
          </span>`,
          function: async () => {
            await this.$refs.logWindow.addLine('Logging in...', 'info', 100);
            await this.$refs.logWindow.addLine(
              'Strange... login infos don´t match',
              'warning',
              3000
            );
          },
        },
        {
          title: "Mit ' probieren",
          instructions: `
          <span>Versuche es jetzt mit einen ' nach dem Passwort: 
            <div class="pt-1">
              E-Mail: <span class="primary--text text--lighten-2 font-weight-bold">test@email.com</span>
              <br/>
              Password: <span class="primary--text text--lighten-2 font-weight-bold">securePassword'</span>
            </div>
            <div class="pt-1">
              Und schauen sie in die <strong class="primary--text text--lighten-1">Logs</strong>
            </div>
          </span>`,
          function: async () => {
            await this.$refs.logWindow.addLine('Logging in...', 'info', 100);
            await this.$refs.logWindow.addLine(
              `An error occurred: PG::SyntaxError: ERROR: unterminated quoted string at or near "'securePassword'' limit 1" LINE 1: ...ers where email = 'user@email.com' and pass = 'securePassword'... ^ : select * from users where email = 'user@email.com' and pass = 'securePassword'' limit 1.Unable to login this user due to unexpected error.`,
              'error',
              3000
            );
            this.currentGuideItem++;
          },
        },
        {
          title: 'Der Server ist gecrasht',
          instructions: `
          <div>Was könnte das bedeuten?</div>
          <div class="pt-2">Die <strong class="primary--text text--lighten-1">Logs</strong> zeigen, dass der <strong>'</strong> charakter etwas durcheinander gebracht hat...</div>
          <div class="pt-1">Im <strong class="primary--text text--lighten-1">Code Snippet</strong> Fenster können Sie beobachten, was sich im Code getan hat</div>`,
          function: async () => {},
        },
        {
          title: 'SQL Injection anwenden',
          instructions: `
          <span>Jetzt versuchen wir die schwachstelle mit diesen Eingaben auszunutzen: <div><strong class="primary--text text--lighten-2">' or 1=1--</strong></div> 
            <div class="pt-1">
              E-Mail: <span class="primary--text text--lighten-2 font-weight-bold">test@email.com</span>
              <br/>
              Password: <span class="primary--text text--lighten-2 font-weight-bold"><strong class="primary--text text--lighten-2">' or 1=1--</strong></span>
            </div>
            <div class="pt-1">
              Und schauen sie in die <strong class="primary--text text--lighten-1">Logs</strong> und <strong class="primary--text text--lighten-1">Code Snippet</strong>
            </div>
          </span>`,
          function: async () => {
            await this.$refs.logWindow.addLine('Logging in...', 'info', 100);
            await this.$refs.logWindow.addLine(
              `Successfully logged in as <strong>test</strong>!`,
              'success',
              3000
            );
          },
        },
      ],
    };
  },

  methods: {
    attemptLogin: async function(e) {
      if (!this.loading && !this.atEnd) {
        this.loading = true;
        console.log(e);
        await this.guide[this.currentGuideItem].function();
        this.currentGuideItem++;
        this.loading = false;
      }
    },
  },

  computed: {
    atEnd() {
      return this.currentGuideItem >= this.guide.length;
    },
  },

  mounted: async function() {
    await this.$refs.logWindow.addLine('[Starting Server...]', 'info', 300);
    await this.$refs.logWindow.addLine('[Server Started]', 'info', 300);
    await this.$refs.logWindow.addLine(
      '<hr class="v-divider theme--dark info darken-1">',
      '',
      0
    );
  },
};
</script>

<style>
html {
  overflow-y: hidden !important;
}
.theme--dark.v-navigation-drawer:not(.v-navigation-drawer--floating)
  .v-navigation-drawer__border {
  background-color: transparent !important;
}
</style>
