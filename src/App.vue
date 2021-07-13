<template>
  <v-app id="inspire">
    <v-app-bar
      app
      shrink-on-scroll
    ><v-row><v-toolbar-title><h2 >    Art from Art Institute of Chicago API </h2></v-toolbar-title></v-row>
      
      
    
    <v-row>
    <v-col cols="12">
      <v-btn
          v-for="link in links"
          :key="link.text"
          :to="link.path"
          text
        >
          {{ link.text }}
        </v-btn>
      </v-col>
    </v-row>
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      links: [
        {
          text: 'About',
          path: '/'
        },
        {
          text: 'Home',
          path: '/data'
        },
      ],
    }),
  }
</script>
<style lang="scss" scoped>
main {
  background-image: url("assets/background.png");
  background-size: 100% 100%;
  background-attachment: fixed;
}
</style>