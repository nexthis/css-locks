<template>
  <v-app id="inspire">
    <v-content>
     <div class="example text-center">Example</div>
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
          </v-col>
        </v-row>
      </v-container>
    </v-content>


    <Modal title="Your CSS" :message="css" :show="modal"  @close="modal = false"/>

  </v-app>
</template>

<script>
import Modal from "./components/Modal";
export default {
  name: "App",
  components: {
    Modal
  },
  data: () => ({
    minFont: 12,
    maxFont: 40,
    minMQ: 360,
    maxMQ: 960,
    css: "",
    modal: false,
  }),

  methods: {
    submit() {
      const { minMQ, maxFont, maxMQ, minFont } = this;
      let m = (maxFont - minFont) / (maxMQ - minMQ);
      let b = minFont - m * minMQ;
      let y = m + b;
      let short = m * 100;
      
    this.css = `
  .example{
    font-size: ${minFont}px;
  }

  @media(min-width:${minMQ}px){
    .example{
      font-size: calc(${short}vw + ${b}px);
    }
  }

  @media(min-width:${maxMQ}px){
    .example{
      font-size: ${maxFont}px;
    }
  }
    `;
    
      this.modal=true;
      this.setCss();
    },

    setCss(){
      const {css} = this;
      if(!document.querySelector('#example')){
        let style = document.createElement('style');
        style.type = 'text/css';
        style.id = 'example'
        style.innerHTML = css;
        document.querySelector('head').appendChild(style);
      }
      else{
        let style = document.querySelector('#example');
        style.innerHTML = css;
      }
    }

  }
};
</script>


