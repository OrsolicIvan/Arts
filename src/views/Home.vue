<template>
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
        :loading="isLoading"
        @input="searchh">
      </v-text-field>
      
        </v-col>

      </v-row>
        <v-row>
          <v-col
            v-for="art in arts"
            :key="art.title" 
            cols="12"
            md="3"
          >
            <v-card outlined>
            <v-list-item three-line>
              <v-list-item-content>     
                <div class="art-title">{{ art.title }}</div>
                <v-list-item-title class="headline mb-1">
                
                </v-list-item-title>
                <v-list-item-subtitle
                  >{{ art.thumbnail.alt_text}}</v-list-item-subtitle
                >
                
              </v-list-item-content>

              <v-list-item-avatar
                tile
                size="80"
                color="grey">
                <v-img  float="left" class="image"  fluid :src="art.thumbnail.lqip"></v-img>
              </v-list-item-avatar>
            </v-list-item>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
    <v-pagination
    total-visible="10"
      v-model="page"
      :length="totalpages"
    ></v-pagination>
          </v-col>
            </v-row>
      </v-container>  
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      arts: [],
      page: 1,
      totalArts: 0,
      totalpages: 0,
      search:'',
      isLoading: false,
    }
  },
created() {
    console.log('created')
    this.getData();
  },
  
  methods: {
    getData() {
      let api = "https://api.artic.edu/api/v1/artworks/search"
      this.axios.get(api, {
        params: {
          'page': this.page,
          'limit':12,
        }
      }) .then((response) => {
  console.log(response.data)
  this.arts = response.data.data
  this.totalArts = response.data.pagination.total
  this.totalpages=response.data.pagination.total_pages
  
      })
    },
    fetchEntriesDebounced() {
      clearTimeout(this._searchTimerId)
      this._searchTimerId = setTimeout(() => {
        this.getData()
      }, 500) 
    },
    searchEntries() {
      this.arts = []
      this.page = 1
      this.fetchEntriesDebounced()
    },
    searchh(){
      let api = "https://api.artic.edu/api/v1/artworks/search"
      this.axios.get(api, {
        params: {
          'q': this.search,
        }
      }) .then((response) => {
  console.log(response.data)
  this.arts = response.data.data
  this.totalArts = response.data.pagination.total
  this.totalpages=response.data.pagination.total_pages
  this.isLoading = false
  
      })
    }
  },
 watch: {
    page: function() {
      this.getData();
    },
    searchh (val) {
      if (!val) {
        return
      }
      this.isLoading = true
      this.searchEntries()
    }
  }
}
</script>
<style>
.image{
  width: 400px;
  height: 400px;
  margin-left: auto;
  margin-right: auto;
  
}
.art-title{
 overflow: hidden;
 display: -webkit-box;
 -webkit-line-clamp: 1;
 -webkit-box-orient: vertical;
}
</style>