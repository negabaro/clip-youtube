<template>
  <div id="app">
    <div id="nav">
      <h1>xxxxxxxxxxxx</h1>
      <div id="player" />
      <youtube
        :video-id="videoId"
        :player-vars="playerVars"
        @ready="ready"
        @ended="ended"
        @error="error"
        ref="youtube"
      />
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> -->
    </div>
    <!-- <router-view /> -->
  </div>
</template>
<script lang="ts">
import Vue from "vue";
import VueYoutube from "vue-youtube";
//let YouTubeIframeLoader = require("youtube-iframe");
//const VueYoutube = require("vue-youtube");
Vue.use(VueYoutube);

export default Vue.extend({
  components: {
    //VueYoutube
  },
  data() {
    return {
      videoId: "",
      start: 0,
      end: 0,
      duration: 0,
      currentLoopCount: 0,
      //player: null,
      playerVars: {
        autoplay: 1
      }
    };
  },
  created() {
    const params = location.pathname.split("/");
    console.log("xxxxxx params", params);

    this.videoId = params[1];
    console.log("this.videoId", this.videoId);
    this.start = Number(params[2]);
    this.end = Number(params[3]);

    //this.loadVideoById();

    //console.log(location.pathname.split("/"));
  },
  computed: {
    //player() {
    //  YouTubeIframeLoader.load((YT: any) => {
    //    const player = new YT.Player("player", {
    //      //startSeconds: '1999',
    //      //height: '390',
    //      //width: '640',
    //      videoId: this.videoId,
    //      //videoId: "Vw-tayLQLuQ",
    //      events: {}
    //    });
    //  });
    //},
    player(): any {
      const youtube: any = this.$refs.youtube;
      console.log("xxxxx youtube", youtube);
      return youtube.player;
    }
  },
  methods: {
    //createFrame() {
    //  return new YT.Player("ytplayer", {
    //    height: "285",
    //    width: "480",
    //    events: {
    //      onReady: onPlayerReady
    //    }
    //  });
    //},
    loadVideoById() {
      console.log("loadVideoById this.player", this.player);
      console.log("loadVideoById this.player", this.videoId);
      this.player.loadVideoById({
        videoId: this.videoId,
        startSeconds: 20,
        endSeconds: 30
      });
    },
    ready(e: any) {
      console.log("ready");
      this.loadVideoById();
    },
    ended(e: any) {
      this.player.seekTo(20);
    },
    error(e: any) {
      console.log("error", e);
    }
  }
});
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
