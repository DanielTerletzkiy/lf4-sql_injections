<template>
  <v-app>
    <v-navigation-drawer app permanent width="360">
      <tutorial-card :guide="guide" :currentGuideItem="currentGuideItem" />
    </v-navigation-drawer>
    <v-main>
      <v-container
        style="display: flex; justify-content: center; align-items: center; height:50%"
      >
        <v-card rounded="lg" elevation="1" width="600">
          <v-card-text
            class="pb-0 d-flex"
            style="justify-content: space-between"
          >
            <div>
              <v-card-title>
                <v-icon left large color="accent">mdi-bank</v-icon>Big Corpo
                Bank
              </v-card-title>
              <v-card-subtitle>
                Trust <strong>us</strong> with <u>your</u> money
                <v-icon style="color: inherit">mdi-currency-usd</v-icon> ;)
              </v-card-subtitle>
            </div>
            <v-list-item style="max-width: 220px;" v-if="atEnd">
              <v-list-item-avatar>
                <v-img
                  src="https://avatars.dicebear.com/api/initials/Daniel%20Terletzkiy.svg"
                />
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-subtitle>
                  Welcome back,
                </v-list-item-subtitle>
                <v-list-item-title>
                  <v-btn
                    @click="openGithub"
                    text
                    style="text-transform: none; padding: 0; font-weight: unset !important; letter-spacing: unset !important; height: 24px; font-size: 18px"
                    >Daniel Terletzkiy</v-btn
                  >
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
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
                <v-btn
                  style="flex: 1"
                  rounded
                  depressed
                  x-large
                  color="accent"
                  type="submit"
                  form="login-form"
                  :loading="loading"
                  :disabled="loading"
                >
                  <v-icon>mdi-wallet-outline</v-icon>Sign In
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card-text>
          <v-card-text v-else>
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
                  Current Balance
                </v-card-title>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-card-subtitle
                  class="pa-0 font-weight-bold primary--text text--lighten-1"
                >
                  Checking
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2"
                    >mdi-currency-usd</v-icon
                  >4,120.86
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2"
                    >mdi-currency-usd</v-icon
                  >5,200.23
                </v-card-subtitle>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-card-subtitle
                  class="pa-0 font-weight-bold primary--text text--lighten-1"
                >
                  Savings
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2"
                    >mdi-currency-usd</v-icon
                  >70,213.65
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle class="pa-0">
                  <v-icon left color="primary lighten-2"
                    >mdi-currency-usd</v-icon
                  >70,213.65
                </v-card-subtitle>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-card-subtitle
                  class="pa-0 font-weight-bold primary--text text--lighten-1"
                >
                  Bitcoin
                </v-card-subtitle>
              </v-col>
              <v-col>
                <v-card-subtitle
                  class="pa-0"
                  :class="
                    `${bitcoin === 0 ? 'text--lighten-1 error' : ''}--text`
                  "
                >
                  <v-icon left color="primary lighten-2"
                    >mdi-currency-btc</v-icon
                  >{{ bitcoin }}
                </v-card-subtitle>
              </v-col>
              <v-col> </v-col>
            </v-row>

            <v-card-text>
              <div style="display: flex; align-items: center;">
                <v-divider class="mr-2" style="max-width: 20px"></v-divider>
                <v-card-subtitle class="pa-1">Bitcoin Transfer</v-card-subtitle>
                <v-divider class="ml-2"></v-divider>
              </div>
              <div style="display: flex;">
                <v-text-field
                  outlined
                  hint="Wallet-ID Autofilled"
                  persistent-hint
                  color="#f7931a"
                  label="Wallet-ID"
                  value="54bd57b7-67af-6db7-ef17-a8c4bef5d3bd"
                />
                <v-btn
                  color="#f7931a"
                  height="56"
                  width="56"
                  depressed
                  text
                  :loading="loading"
                  :disabled="loading || bitcoin === 0"
                  @click="sendBitcoin"
                >
                  <v-icon large color="#f7931a">mdi-bitcoin</v-icon>
                </v-btn>
              </div>
            </v-card-text>
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
      bitcoin: 20.3890234,
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
              1000
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
              1000
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
              `Successfully logged in as <a class="primary--text text--lighten-1"><strong>Daniel Terletzkiy</strong></a>!`,
              'success',
              1000
            );
          },
        },
        {
          title: 'Fertig!',
          instructions: `
          <span>Und so einfach war es, die schwachstelle auszunutzen.<br/>Jetzt haben sie die Kontrolle über dieses 'Konto'</span>`,
          function: async () => {},
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
    openGithub() {
      window.open('https://github.com/DanielTerletzkiy', '_blank');
    },
    sendBitcoin: async function() {
      this.loading = true;
      await this.$refs.logWindow.addLine(
        'Transferring Bitcoin...',
        'info',
        300
      );
      await this.$refs.logWindow.addLine(
        'All Bitcoin transferred!',
        'success',
        1000
      );
      this.loading = false;
      this.bitcoin = 0;
    },
  },

  computed: {
    atEnd() {
      return this.currentGuideItem >= this.guide.length - 1;
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

::-webkit-scrollbar {
  width: 4px;
  height: 4px;
}

::-webkit-scrollbar-track {
  background-color: rgba(0, 0, 0, 0.086);
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
}

.theme--dark.v-navigation-drawer:not(.v-navigation-drawer--floating)
  .v-navigation-drawer__border,
.theme--dark.v-navigation-drawer {
  background-color: #242731 !important;
}
.theme--dark.v-list-item:not(.v-list-item--active):not(.v-list-item--disabled),
.theme--dark.v-btn {
  color: hsla(0, 0%, 100%, 0.7) !important;
}
</style>
