<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >


      <v-btn
        href="https://lukasmarkert.de"
        target="_blank"
        text
      >
        <span class="ml-2">Home</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <UploadPdf/>
    </v-main>
  </v-app>
</template>

<script>
import UploadPdf from "@/components/UploadPdf";

export default {
  name: 'App',

  components: {
    UploadPdf,
  },

  data: () => ({
    //
  }),
};
</script>
