<template>
  <v-card width="500" flat height="240">
    <v-card-subtitle class="pa-2">
      Logs
    </v-card-subtitle>
    <v-divider class="mx-2"></v-divider>
    <div class="pa-2" style="height: 84%">
      <div
        style="min-height: 100%; max-height: 100%; overflow: auto; font-family: monospace;"
      >
        <v-card-text v-html="logHtml"></v-card-text>
        <div ref="logEnd" class="pt-1"/>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  components: {},

  props: {},

  data: () => ({
    logHtml: '',
  }),

  methods: {
    addLine(text, color, time) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(this.renderLine(text, color));
        }, time);
      });
    },
    renderLine(text, color) {
      this.logHtml += `<span class="${color}--text">${text}</span><br/>`;
      return null;
    },
  },

  computed: {},

  watch: {
    logHtml() {
      setTimeout(() => {
        const el = this.$refs.logEnd;
        console.log(el);
        el.scrollIntoView({
          behavior: 'smooth',
        });
      }, 10);
    },
  },

  mounted: async function() {},
};
</script>

<style></style>
