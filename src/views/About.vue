<template>
<v-container >
<v-row>
  <v-col cols="12">
    <h2>Explore thousands of artworks in the museum’s wide-ranging collection<br>
     <br> from our world-renowned icons to lesser-known gems from every corner of the globe<br>
      <br>as well as our books, writings, reference materials, and other resources.</h2>

    <v-dialog
      v-model="addDialog" 
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="orange"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Add review
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Add review
        </v-card-title>

        <v-card-text>
          <Form></Form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="addDialog = false; successAlert=true;"
          >
            Submit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-alert type="success" v-model="successAlert" dismissible>
      Review added successfully!
      </v-alert>
      </v-col>
    </v-row>
   </v-container>
</template>

<script>
import Form from "../components/Form.vue";

export default {
  components:{Form},
      data(){
        return{
          addDialog: false,
          successAlert: false 
        }
      }
    
  }
</script>
<style scoped>
h1 {text-align: center;}
</style>

