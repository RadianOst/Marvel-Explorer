<template>
  <v-bottom-nav
    :value="true"
    fixed
  >
    <v-btn
      flat
      @click="changeOffset(false)"
      :disabled="!canGoBack"
    >
      <!--<span>Previous</span>-->
      <v-icon>navigate_before</v-icon>
    </v-btn>

    <v-btn flat disabled>{{ pagination.description }}</v-btn>

    <v-btn
      flat
      @click="changeOffset(true)"
      :disabled="!canGoForward"
    >
      <!--<span>Next</span>-->
      <v-icon>navigate_next</v-icon>
    </v-btn>
  </v-bottom-nav>
</template>

<script>
  export default {
    name: "BottomNavigation",
    props: ['pagination'],
    methods: {
      changeOffset(increment) {
          this.$emit('change-offset', increment);
      }
    },
    computed: {
      canGoBack() {
        return this.pagination.offset > 0
      },
      canGoForward() {
        return this.pagination.offset + this.pagination.limit < this.pagination.totalItems
      }
    }
    }
</script>

<style scoped>

</style>