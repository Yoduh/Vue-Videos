<template>
  <div class="container">
    <search-bar @termChange="onTermChange"></search-bar>
    <div class="row">
      <video-detail :video="selectedVideo" />
      <video-list :videos="videos" @videoSelect="onVideoSelect"></video-list>
    </div>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';
import axios from 'axios'
const API_KEY = 'AIzaSyByCwz4Wa23aATnfPpOO4_upevua7hvezs';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  
  data() {
    return {
      videos: [],
      selectedVideo: null
    }
  },
  methods: {
    onTermChange(searchTerm) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      .then(response => {
        this.videos = response.data.items
      });
    },

    onVideoSelect(video) {
      this.selectedVideo = video;
    }
  }
}
</script>

<style>

</style>
