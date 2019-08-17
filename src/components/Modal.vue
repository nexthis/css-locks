<template>
  <v-row justify="center">
    <v-dialog v-model="show" persistent max-width="500">

      <v-card>
        <v-card-title class="headline">{{title}}</v-card-title>
        <v-card-text  >
          <code style=" width: 100%;">
            {{message}}
          </code>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="$emit('close')">ok</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  export default {
    props:{
      title: String,
      message: String,
      show: Boolean,
    },

  }
</script>