<template >
  <v-app-bar app :elevation="2" color="grey">
    <v-app-bar-title>VAppManager</v-app-bar-title>
    <v-spacer></v-spacer>
    <v-btn @click="activateInvisibleInput">
      install new app
    </v-btn>
    <input @change="installVapp" class="invisible-input" type="file" ref="invisibleInput">
  </v-app-bar>
</template>

<script>
import { mapActions } from 'vuex';
const production = 'http://' + window.location.hostname
const dev = 'http://127.0.0.1:5000'

export default {
  data: () =>{
    return {
      file: {},
      domain: dev
    }
  },
  methods: {
    ...mapActions({
      installVApp: 'camera/installVApp'
    }),
    activateInvisibleInput() {
      this.$refs.invisibleInput.click()
    },
    installVapp(){
      let file = this.$refs.invisibleInput.files[0]
      const queryInfo = {file: file, domain: this.domain}
      this.installVApp(queryInfo)
      this.$refs.invisibleInput.value = null
    }
  }
}
</script>

<style>
.invisible-input {
  display: none;
}
</style>