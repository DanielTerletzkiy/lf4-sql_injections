<template>
  <v-card color="#242731" width="600" flat height="100%">
    <v-card-text class="pa-0">
      <v-card-title class="pa-2">
        Guide
      </v-card-title>
    </v-card-text>
    <v-divider class="mx-2"></v-divider>
    <div class="pa-2">
      <v-timeline dense class="ml-n6">
        <v-slide-x-reverse-transition group hide-on-leave>
          <v-timeline-item
            v-for="(item, i) in guide"
            :key="item.title"
            fill-dot
            :color="i === currentGuideItem ? 'primary' : 'secondary'"
            v-show="i <= currentGuideItem"
          >
            <v-card flat color="transparent">
              <v-card-text class="pa-0">
                <v-card-title>{{ item.title }}</v-card-title>
                <v-card-subtitle>{{ item.instructions }}</v-card-subtitle>
              </v-card-text>
            </v-card>
          </v-timeline-item>
        </v-slide-x-reverse-transition>
      </v-timeline>
    </div>
  </v-card>
</template>

<script>
export default {
  components: {},

  props: {
    guide: Array,
    currentGuideItem: Number,
  },

  data: () => ({}),

  methods: {},

  computed: {},

  mounted: async function() {},
};
</script>

<style></style>
