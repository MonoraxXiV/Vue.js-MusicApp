<template>
  <!--html code-->
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="songTitle">{{ current.title }} - <span>{{current.artist}}</span></h2>
        <!--placing controls here-->
        <div class="controls">
          <button class="previous">Previous</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="Pause">Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
/*Javascript code*/
export default {
  name: 'App',
  /*  data works similar to state in react in this case*/
  data() {
    return {
      current: {
  /*      title: 'SONG TITLE'*/
      },
      isPlaying: false,
      index: 1,
      songs: [
        {
          /*Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/enigmatic*/
        title: 'Enigmatic',
          artist: 'Bensound',
          src: require('./assets/bensound-enigmatic.mp3')
        },
        {
         /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/epic*/
          title: 'Epic',
          artist: 'Bensound',
          src: require('./assets/bensound-epic.mp3')
        },
        {
          /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/evolution*/
          title: 'Epic',
          artist: 'Bensound',
          src: require('./assets/bensound-evolution.mp3')
        }
      ],
      player: new Audio(),
    }
  },
  methods:{
    play(song){
      if (typeof song.src != "undefined" ){
      this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying=true;
    },
    Pause(){
      this.player.pause();
      this.isPlaying=false;
    },
  },
  created (){
      this.current = this.songs[this.index];
      this.player.src = this.current.src;


  }

}
</script>

<style>
/*css code*/

* {
  /*removes browser default settings*/
  margin: 0;
  padding: 0;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background-color: darkslateblue;
  color: white;
}
h2{
  padding: 3px;
}
</style>
