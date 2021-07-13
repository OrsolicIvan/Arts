<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="Name"
            :counter="10"
            label="Name"
            required
          ></v-text-field>
        </v-col>

    

        <v-col
          cols="12"
          md="4"
        >
        </v-col>
      </v-row>
    </v-container>
    <v-container fluid>
    <v-textarea
      clearable
      clear-icon="mdi-close-circle"
      label="Review"
    ></v-textarea>
  </v-container>
  </v-form>
</template>
<script>

export default {
  data(){
    return{
      Name: ""
    }
  }
}

</script>