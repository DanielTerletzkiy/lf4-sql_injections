<template>
  <v-card color="#242731" width="500" flat height="240">
    <v-card-subtitle class="pa-2">
      Code Snippet
    </v-card-subtitle>
    <v-divider class="mx-2"></v-divider>
    <div class="pa-2" style="height: 84%">
      <div style="height: 100%; overflow: auto; font-family: monospace;">
        <v-card-text>
          <pre v-highlightjs="`SELECT *
  FROM users
  WHERE email = '${email}'
  AND pass  = '${password}' LIMIT 1
`"><code class="sql"></code></pre>
        </v-card-text>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  components: {},

  props: {
    email: String,
    password: String,
  },

  data: () => ({
    codeHtml: '',
  }),

  methods: {
    addLine(text, color) {
      this.codeHtml += `<span class="${color}--text">${text}</span><br/>`;
    },
  },

  computed: {},

  mounted: async function() {},
};
</script>

<style>
.theme--dark.v-application code {
  background-color: transparent !important;
}
</style>
