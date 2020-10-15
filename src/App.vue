<template>
  <v-app>
    <v-container>
      <br />
      <v-text-field dense outlined label="word code" type="text" v-model="form.wordCode"></v-text-field>
      <v-text-field dense outlined label="rus" type="text" v-model="form.rusText"></v-text-field>
      <v-text-field dense outlined label="ukr" type="text" v-model="form.ukrText"></v-text-field>
      <v-text-field dense outlined label="eng" type="text" v-model="form.engText"></v-text-field>

      <v-btn :disabled="!form.wordCode || !form.rusText || !form.ukrText || !form.engText" @click="writeNewWord">Write</v-btn>
      <br />
      <p>{{ result }}</p>
    </v-container>
    <!-- <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40" />

        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100" src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png" width="100" />
      </div>

      <v-spacer></v-spacer>

      <v-btn href="https://github.com/vuetifyjs/vuetify/releases/latest" target="_blank" text>
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <HelloWorld />
    </v-main> -->
  </v-app>
</template>

<script>
// import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    // HelloWorld
  },

  data: () => ({
    form: {
      wordCode: "",
      rusText: "",
      ukrText: "",
      engText: ""
    },
    result: ""
  }),
  methods: {
    writeNewWord() {
      let me = this;
      console.log(me.form);
      me.$axios.post(`/localization/writeNewWord/`, me.form).then((response) => {
        me.result = response.data;
        me.form.wordCode = "";
        me.form.rusText = "";
        me.form.ukrText = "";
        me.form.engText = "";
        setTimeout(() => {
          me.result = "";
        }, 1000);
      });
    }
  }
};
</script>
