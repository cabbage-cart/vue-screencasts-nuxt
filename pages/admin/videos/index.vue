<template>
  <v-container>
    <h1>Video List</h1>
    <v-btn text to="/admin/videos/new">Add Video</v-btn>

    <VideoTableWithSearch :videos="videos" 
                          :headers="headers" 
                          :customClickAction="goToVideoShow"
                          :dense="true"
                          :showExpand="true"
                          :itemsPerPage="20" />
  </v-container>
</template>

<script>
  import VideoTableWithSearch from '@/components/VideoTableWithSearch'
  import { mapState } from 'vuex';
  export default {
    components: {
      VideoTableWithSearch
    },
    computed: {
      ...mapState({
        videos: state => state.videos.videos
      }),
      headers(){
        return [
          {text: 'Name', value: 'name'},
          {text: 'Pro', value: 'pro', width: '70px'},
          {text: 'Date', value: 'sortable_published_at'},
          {text: 'Duration', value: 'duration'},
          {text: 'Course', value: 'courseName'},
          {text: 'Actions', value: 'actions', sortable: false, width: "300px"},
        ]
      },
    },
    methods: {
      goToVideoShow(video) {
        this.$router.push(`/admin/videos/${video.id}`)
      },
    },
    head(){
      let title = `VueScreencasts - ${this.videos.length} videos available`
      let description = "Come browse our ever-growing library of Vue-related videos"
      return {
        title: title,
        meta: [
          {hid: 'description', property: 'description', content: description},
          {hid: 'og-description', property: 'og:description', content: description},
          {hid: 'twitter-description', property: 'twitter:description', content: description},
          {hid: 'og-title', property: 'og:title', content: title},
          {hid: 'twitter-title', property: 'twitter:title', content: title},
        ]
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>