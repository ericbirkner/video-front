<script>
import axios from 'axios';
import Video from '../components/Video.vue';
import AddVideo from '../components/AddVideo.vue';
import Loading from '../components/Loading.vue';
import { reactive, toRefs, computed, onMounted, ref } from "vue";
export default {
  components: {
    Video,
    AddVideo,
    Loading
  },
  setup() {
    const state = reactive({
      videos: [],
    });

    const getVideos = () => {
      axios.get('http://ec2-44-210-126-6.compute-1.amazonaws.com/api/videos')
      .then(response => {
        console.log(response.data);
        state.videos = response.data
      })
    }
    const deleteVideo = (vid)=>{
      alert(vid)
    }    

    onMounted(() => {
         console.log('se llama api');
         getVideos();
    });

    return {
      state,
      deleteVideo,
      getVideos
    };
    
  }
}
</script>

<template>
 <div class="container">
  <div class="row pt-5">
    <div class="col-12">
      <add-video @callVideos="getVideos"></add-video>
    </div>
  </div>
  <div class="row justify-content-center p-3">
    <template v-if="state.videos.length>0">
      <div class="col-12 col-md-6 col-lg-4" v-for="video in state.videos" :key="video.id">
        <Video :data="video"></Video>
      </div>
    </template>    
    <div v-else class="col-12">
      <loading></loading>
    </div>
  </div>
 </div>
</template>
