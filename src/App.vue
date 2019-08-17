<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Css locks (px)</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field v-model="minFont" type="number" label="Min font size"></v-text-field>
                  <v-text-field v-model="maxFont" type="number" label="Max font size"></v-text-field>
                  <v-text-field v-model="minMQ" type="number" label="Min media query"></v-text-field>
                  <v-text-field v-model="maxMQ" type="number" label="Max media query"></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn @click="submit" color="primary">Calculate</v-btn>
              </v-card-actions>
            </v-card>
            <div v-html="css"></div>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
    <div class="test">test</div>
  </v-app>
</template>

<script>
import Modal from "./components/Modal";
export default {
  name: "App",
  components: {},
  data: () => ({
    minFont: 12,
    maxFont: 40,
    minMQ: 360,
    maxMQ: 960,
    css: ""
  }),

  methods: {
    submit() {
      const { minMQ, maxFont, maxMQ, minFont } = this;
      let m = (maxFont - minFont) / (maxMQ - minMQ);
      let b = minFont - m * minMQ;
      let y = m + b;
      let short = m * 100;
      
      this.css = `
        font-size: ${minFont}px;

        @media(min-width:${minMQ}px){
          font-size: calc(${short}vw + ${b}px);
        }

        @media(min-width:${maxMQ}px){
          font-size: ${maxFont}px;
        }
      `;
      
    }
  }
};
</script>


<style lang="scss" scoped>
.test {
  font-size: 12px;
  @media (min-width: 360px) {
    font-size: calc(14.666666666666666vw + -40.8px);
  }
  @media (min-width: 960px) {
    font-size: 100px;
  }
}
</style>