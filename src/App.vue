<template>
  <div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail v-bind:video="selectedVideo" />
      <VideoList
        v-on:videoSelectItem="onVideoSelect"
        :videos="myListOfVideos"
      />
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import SearchBar from './components/SearchBar'
  import VideoList from './components/VideoList'
  import VideoDetail from './components/VideoDetail'

  import {response} from './data'

  // v-on = @
  // v-bind = :
  const API_KEY = process.env.VUE_APP_API_KEY

  export default {
    name: 'App',
    components: {
      SearchBar: SearchBar,
      VideoList: VideoList,
      VideoDetail: VideoDetail
    },
    data () {
      return {
        myListOfVideos: [],
        selectedVideo: null
      }
    },
    methods: {
      onTermChange (searchTerm)  {
        // this.myListOfVideos = response.items
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
        }).then(response => this.myListOfVideos = response.data.items)
        
      },
      onVideoSelect (video) {
        this.selectedVideo = video
      }
    }
  }
</script>