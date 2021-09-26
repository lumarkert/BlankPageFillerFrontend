<template>
  <v-container>
    <v-sheet :elevation="15"
             class="mx-auto mt-2"
             height="1000px"
             width="1000px">
      <v-row class="text-center">

        <v-col class="mb-4">
          <h1 class="display-2 font-weight-bold mb-3">
            Pdf Blank Page Filler
          </h1>

          <p class="subheading font-weight-regular">
            With this tool you can add a blank page after every page in a pdf.
          </p>
        </v-col>
      </v-row>
      <v-row class="text-center">
        <v-col class="mx-4 pa-4">
          <v-file-input accept=".pdf" id="file" v-model="file" v-on:change="handleFileUpload()"/>
        </v-col>

      </v-row>
      <v-row class="text-center">
        <v-col class="mb-4">
          <v-btn class="mx-4" v-on:click="submitFile()">Submit</v-btn>
          <v-btn class="mx-4" :disabled="!fileExists" :href="this.link">Download</v-btn>
        </v-col>


      </v-row>
      <div>
        <pdf :disabled='!fileExists' :src='this.link'></pdf>
      </div>
    </v-sheet>

  </v-container>
</template>

<script>
import pdf from 'vue-pdf'

const axios = require('axios');

export default {
  components: {
    pdf
  },
  data() {
    return {
      file: '',
      link: '',
      fileExists: false
    }
  },
  name: "UploadPdf",
  methods: {
    handleFileUpload() {
      //this.fileExists = true;
      //this.link = window.URL.createObjectURL(this.file)

    },
    submitFile() {
      let formData = new FormData();
      formData.append('file', this.file);
      console.log(formData)
      let address_pdf = process.env.NODE_ENV === 'production' ? 'https://pdf-back.lukasmarkert.de'
          : 'http://localhost:2222/pdf'

      axios.post(address_pdf, formData, {
        responseType: 'arraybuffer',
        headers: {'Content-Type': 'multipart/form-data'}
      }).then(response => {
        console.log(response);
        let blob = new Blob([response.data], {type: 'application/pdf',})
        this.fileExists = true;
        this.link = window.URL.createObjectURL(blob)
        window.open(this.link);
      });
    }
  }
}
</script>

<style scoped>

</style>
