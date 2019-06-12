<template>
    <div class="container">
        <div class="logo-box">
        <img src="./assets/icon-vid.svg" class="logo">
        <h4 class="title">YouTube Search</h4>
        </div>
        <SearchBar @termChange="onTermChange"></SearchBar>
       <div class="row">
        <VideoDetail :video="selectedVideo" />
        <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import SearchBar from './components/SearchBar'
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'

const API_KEY = 'AIzaSyBQHdyzJQFWXMuuxIhP-kBXHj3a325tJb0'

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
        onVideoSelect(video) {
            this.selectedVideo = video
        },
        onTermChange(searchTerm) {
            axios
            .get('https://www.googleapis.com/youtube/v3/search?', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm
                }
            })
            .then(response => {
                this.videos = response.data.items
            })
            //  .catch(err => { console.log(err); })
        }
    }
}
</script>

<style>
.title {
    display: flex;
    align-items: center;
    justify-content: center 
}
.logo {
    height: 128px;
    width: 128px;
    display: block;
    margin-left: auto;
    margin-right: auto;
    padding: 10px;
}
</style>

