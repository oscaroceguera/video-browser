<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList :videos="myListOfVideos" />
  </div>
</template>

<script>
  import axios from 'axios'
  import SearchBar from './components/SearchBar'
  import VideoList from './components/VideoList'

  // v-on = @
  // v-bind = :

  const API_KEY = 'AIzaSyBSmJyowEg2kWa19Axp1kcflKncqAG_P24'

  export default {
    name: 'App',
    components: {
      SearchBar: SearchBar,
      VideoList: VideoList
    },
    data () {
      return {
        myListOfVideos: []
      }
    },
    methods: {
      onTermChange (searchTerm)  {
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
        }).then(response => this.myListOfVideos = response.data.items)
      }
    }
  }
</script>