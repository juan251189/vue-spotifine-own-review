<template>
<div id="app">
  <div class="container-fluid">
    <div class="header-page">
      <h1>Guitar<span>Covers</span></h1>
    </div>

    <div class="main" >
      <section id="front" class="container-fluid">
        <div class="row">
        <div class="col-sm-4 col-6 col-md-4" style="border:1px solid white;">
          <img class="image-front" :src="current.image" alt="">
        </div>

        <div class="col-sm-8 col-6 col-md-8" style="border:1px solid white;">
          <h1>{{current.title}}</h1>  <h3>{{current.artist}}</h3>
          <p>{{current.paragraph}}</p>

        </div>
</div>
      </section>




      <div class="title-player"></div>
      <div class="image-player"></div>



      <div class="list-container">

        <div class="row list-header">
          <div class="col-sm-6 col-7" style="border:1px solid white;">title</div>
          <div class="col-sm-6 col-5" style="border:1px solid white; " >album</div>
        </div>
        <div class="list-songs" v-for="(song,i) in songs" :key="i">
          <div class="row">

            <div class="col-sm-6 col-7" style="border:1px solid white;"><span class="icon"><i class="fab fa-itunes-note " /></span>
              <div class="content">
                <a>
                  <p class="list-song-title" @click="selectSong(song,i)" :class="(song.src === current.src) ? 'playing' :''">{{song.title}}</p>
                </a>
                <p>{{song.artist}}</p>
              </div>
            </div>
            <div class="col-sm-6 col-5" style="border:1px solid white;" >
              <p :class="(current.src == song.src) ? 'playing' : ''">{{song.album}}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="buttons">
        <button >Random</button>
        <button @click="prev">prev</button>
        <button class="far fa-pause-circle" v-if="isPlaying" @click="pauseSong"></button>
        <button class="far fa-play-circle" v-else @click="playSong"></button>
        <button @click="next">Next</button>
        <button >Repeat</button>

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
          album: " to be research",
          src: require("./assets/songs/metallica/forwhom.mp3"),
          image: require("./assets/songs/metallica/ride-the-lightning.jpg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "Metallica",
          title: "Creeping Death",
          album: " to be research",
          src: require("./assets/songs/metallica/creeping-death.mp3"),
          image: require("./assets/songs/metallica/ride-the-lightning2.jpeg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "Megadeath",
          title: "A tout le monde",
          album: " to be research",
          src: require("./assets/songs/megadeath/a-toute-le-monde.mp3"),
          image: require("./assets/songs/megadeath/Megadeth-Youthanasia.jpg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "Scorpions",
          title: "Still Loving You",
          album: " to be research",
          src: require("./assets/songs/scorpions/still-loving-you.mp3"),
          image: require("./assets/logo.png"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "The Eagles",
          title: "Hotel California Solo",
          album: " to be research",
          src: require("./assets/songs/hotel-california-solo.mp3"),
          image: require("./assets/logo.png"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        }
      ],
      isPlaying: false,
      player: new Audio(),
      index: 0



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
*/
      if (Object.keys(this.current).length === 0) {
        this.current = this.songs[0];
        console.log(this.current);
        this.player.src = this.current.src;
        this.player.play();
        this.isPlaying = true;
      } else {
        this.player.play();
        this.isPlaying = true;
      }

    },
    pauseSong() {
      this.player.pause();
      this.isPlaying = false;

    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
        console.log(this.current);
      }
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      this.player.play();
    },
    next() {



      this.index++;
      if (this.index > this.songs.length - 1) {
        //this.index=this.songs.length-1;
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      this.player.play();
      console.log(this.index);
    },
    selectSong(song, i) {
      if (typeof song.src != "undefined") {
        this.current = song;
      }

      this.player.pause();
      this.current = song;
      this.player.src = this.current.src;
      this.player.play();
      this.isPlaying = true;
      this.index = i;
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
  padding: 0;
  background-color: #131313;

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
  z-index: 1;
}

.header-page h1 {
  color: #FFFFFF;
  font-weight: 400;
}

.header-page span {
  color: #41a8e2;
  font-weight: 600;
}

.main {
  padding-top: 80px;

  height: 1500px;
}

#front {
  background-image: linear-gradient(#525252, #2C2C2C);
  height: 300px;
  padding: 35px;
  overflow-y:hidden;
  color: #C2C2C2;

  font-family: "montserrat",sans-serif;


}
#front h1{
  font-size: 70px;
  color: #f3f3f3;

  font-weight: 700;
}
#front h3{
  color:#F3F3F3;

}

#front .image-front{
  max-height: 430px;
  max-width:275px;
  padding-left: 0px;
  margin-left: 0px;

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
.list-header{
  padding: 10px 45px;

  color:#f3f3f3;
  border-bottom: 1px solid #383838;

}
.list-container {
  background-color: #131313;
  height: 100vh;
}

.list-song-title {
  font-size: 17px;
  cursor: pointer;
}

.list-songs .icon {
  float: left;
  margin-right: 8px;
  position: relative;

}

.list-songs .content {
  margin-top: 0px;
  margin-left: 21px;
}

.playing {
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
