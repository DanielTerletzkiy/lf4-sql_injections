<template>
  <v-card color="#242731" width="400" flat height="240">
    <v-card-subtitle class="pa-2">
      Logs
    </v-card-subtitle>
    <v-divider class="mx-2"></v-divider>
    <div class="pa-2" style="height: 84%">
      <div
        style="min-height: 100%; max-height: 100%; overflow: auto; font-family: monospace;"
      >
        <v-card-text v-html="logHtml"></v-card-text>
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
      return new Promise((resolve)=> {
        setTimeout(()=> {
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

  mounted: async function() {},
};
</script>

<style></style>
