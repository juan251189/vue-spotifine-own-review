<template>
<div id="app">
  <div class="container-fluid">
    <div class="header-page">
      <h1>Spoti<span>Fine</span></h1>
    </div>

    <div class="main">
    <div class="title-player"></div>
    <div class="image-player"></div>



  <div class="list-container">


    <div class="list-songs" v-for="(song,i) in songs" :key="i">
      <div class="row">

      <div class="col-sm-6"><span class="icon"><i class="fab fa-itunes-note " /></span>
      <div class="content">
        <a>
          <p class="list-song-title"
          @click="selectSong(song,i)"
          :class="(song.src === current.src) ? 'playing' :''"

          >{{song.title}}</p>
        </a>
        <p>{{song.artist}}</p>
      </div>
      </div>
      <div class="col-sm-6">
        <p style="text-align:center;">{{song.album}}</p>
      </div>
      </div>
    </div>
  </div>

    <div class="buttons">
      <button @click="prev">prev</button>
      <button class="far fa-pause-circle" v-if="isPlaying" @click="pauseSong"></button>
      <button class="far fa-play-circle" v-else @click="playSong"></button>
      <button @click="next">Next</button>
    </div>


</div>
  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      current: {},
      songs: [{
          artist: "Metallica",
          title: "For whom the bell tolls",
          album:" to be research",
          src: require("./assets/forwhom.mp3")
        },
        {
          artist: "Metallica",
          title: "Creeping Death",
          album:" to be research",
          src: require("./assets/creeping-death.mp3")
        },
        {
          artist: "Megadeath",
          title: "A tout le mond",
          album:" to be research",
          src: require("./assets/a-toute-le-monde.mp3")
        },
        {
          artist: "Scorpions",
          title: "Still Loving You",
          album:" to be research",
          src: require("./assets/still-loving-you.mp3")
        },
        {
          artist: "The Eagles",
          title: "Hotel California Solo",
          album:" to be research",
          src: require("./assets/hotel-california-solo.mp3")
        }
      ],
      isPlaying: false,
      player:new Audio(),
      index:0



    }
  },


  methods: {


    playSong() {
    /*  if (typeof song.src !="undefined"){
        this.current=song;
      }
      this.player.src=this.current.src;
      this.player.play();
      this.isPlaying=true;
!
*/    if (Object.keys(this.current).length === 0){
      this.current=this.songs[0];
      console.log(this.current);
      this.player.src=this.current.src;
      this.player.play();
      this.isPlaying=true;
    }else{
    this.player.play();
      this.isPlaying=true;
}

    },
    pauseSong() {
      this.player.pause();
      this.isPlaying=false;

    },
    prev(){
      this.index--;
      if(this.index<0){
        this.index=this.songs.length-1;
        console.log(this.current);
      }
      this.current=this.songs[this.index];
      this.player.src=this.current.src;
      this.player.play();
    },
    next(){



      this.index++;
      if (this.index >this.songs.length-1){
        //this.index=this.songs.length-1;
        this.index=0;
      }
      this.current=this.songs[this.index];
      this.player.src=this.current.src;
      this.player.play();
      console.log(this.index);
    },
    selectSong(song,i){
      if (typeof song.src !="undefined"){
        this.current=song;
      }

      this.player.pause();
      this.current=song;
      this.player.src=this.current.src;
      this.player.play();
      this.isPlaying=true;
      this.index=i;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin: 0;
  padding:0;
  background-color: #272727;
}

.container-fluid {
  padding: 0;
  width: 100vw;
  justify-content: center;
}

.header-page {
  display: flex;
  min-height: 80px;
  width: 100vw;
  justify-content: space-around;
  align-items: center;

  padding: 0 12px;

  background-color: #090909;

  font-size: 18px;
  font-family: 'montserrate', sans-serif;

  position: fixed;
}

.header-page h1 {
  color: #FFFFFF;
  font-weight: 400;
}

.header-page span {
  color: #41a8e2;
  font-weight: 600;
}

.main{
padding-top: 100px;

height: 1500px;
}
.list-songs {



  width: 100vw;
  color: #F3F3F3;

  font-size: 13px;
  font-family: 'montserrat', sans-serif;
  font-weight: 400;
  line-height: 22px;

  padding: 10px 45px;


}
.list-container{
    background-image:linear-gradient(#1F1F1F,#131313);
    height: 100vh;
}
.list-song-title{
  font-size: 17px;
  cursor: pointer;
}

.list-songs .icon {
  float: left;
  margin-right: 8px;
  position: relative;

}
.list-songs .content{
  margin-top: 0px;
  margin-left: 21px;
}

.playing{
  color: #4ef002;

}

.buttons {
  position: fixed;
  bottom: 0;
  display: flex;
  height: 80px;
  width: 100vw;

  justify-content: center;
  align-items: center;
  border: 1px solid white;

  background-color: #282828;

}

.buttons button {
  position: relative;
  height: 25px;
  background-color: none;
  margin: 0 15px;


}


.fa-pause-circle:hover {

  font-size: 1em;
  transition: 1s;
}
</style>
