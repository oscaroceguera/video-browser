<template>
  <ul class="list-group col-md-4">
    <VideoListItem
      v-for="video in videos"
      v-bind:video="video"
      :key="video.etag"
      @videoSelectItem="onVideoSelectList"
    >
    </VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem'

export default {
  name: 'VideoList',
  components: {
    VideoListItem
  },
  props: ['videos'],
  methods: {
    onVideoSelectList(video) {
      this.$emit('videoSelectItem', video)
    }
  }
}
</script>

<style>

</style>
