<template>
  <v-app>
    <v-app-bar
      app
      color="white"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="SpaceX"
          class="shrink mr-2 over"
          contain
          src="./assets/spacex.png"
          transition="scale-transition"
          width="250"
          @click="$router.push('/')"
        />
      </div>
      <v-spacer />
      <v-btn
        href="https://www.spacex.com"
        target="_blank"
        text
        color="primary"
      >
        <span class="mr-2">Go to SpaceX</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>

    <div id="footer">
      <v-footer
        class="font-weight-medium"
      >
        <v-col
          class="text-center pb-1"
          cols="12"
        >
          <strong>SpaceX - Management</strong>
        </v-col>
         <v-col
          class="text-center pa-0 ma-0"
          cols="12"
        >
          <p>{{ new Date().getFullYear() }}</p>
        </v-col>
      </v-footer>
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'App'
};
</script>

<style lang="scss">
.over {
  cursor: pointer;
}
#footer {
  display: table-row;
}
#footer p {
  font-size: 14px;
}
</style>
