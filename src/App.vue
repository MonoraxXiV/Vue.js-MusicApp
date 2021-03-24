<template>
  <!--html code-->
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="songTitle">{{ current.title }} - <span>{{current.artist}}</span></h2>
      </section>
        <!--placing controls here-->
        <div class="controls">
          <button class="previous" @click="Previous"> ◄ Previous</button>
          <button class="play" v-if="!isPlaying" @click="play"> Play</button>
          <button class="pause" v-else @click="Pause">  Pause</button>
          <button class="next" @click="Next">Next ► </button>
        </div>

      <section class="playlist">
        <h3>Playlist</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src === current.src)? 'song playing' : 'song'">
       {{song.number}} {{song.title}} - {{song.artist}}
        </button>
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

      },
      isPlaying: false,
      index: 0,
      songs: [
        {
          /*Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/enigmatic*/
          number:'1',
        title: 'Enigmatic',
          artist: 'Bensound',
          src: require('./assets/bensound-enigmatic.mp3')
        },
        {
         /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/epic*/
          number:'2',
          title: 'Epic',
          artist: 'Bensound',
          src: require('./assets/bensound-epic.mp3')
        },
        {
          /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/evolution*/
          number:'3',
          title: 'Evolution',
          artist: 'Bensound',
          src: require('./assets/bensound-evolution.mp3')
        },
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

      this.player.addEventListener('ended',function(){
        this.index++;
        if (this.index > this.songs.length-1){
          this.index=0;
        }
        /*here we change the index so another song will play, you forgot this earlier which is why next wouldn't work'*/
        this.current=this.songs[this.index];
        this.play(this.current)

      }.bind(this))
      this.isPlaying=true;
    },
    Pause(){
      this.player.pause();
      this.isPlaying=false;
    },
    Next(){
      this.index++;
      if (this.index > this.songs.length-1){
        this.index=0;
      }
      /*here we change the index so another song will play, you forgot this earlier which is why next wouldn't work'*/
      this.current=this.songs[this.index];
      this.play(this.current)
    },
    Previous(){
      this.index--;
      /*if less than 0, bring back to the end of the list*/
      if (this.index < 0){
          this.index= this.songs.length-1;
      }
      this.current=this.songs[this.index];
      this.play(this.current)
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
/*attempt to import font*/
@import url('https://fonts.googleapis.com/css2?family=DotGothic16&display=swap');
* {
  /*removes browser default settings*/
  margin: 0;
  padding: 0;
}
body{
  background-color: #554c7b;
  color: white;
  background-image: image("https://cdn.discordapp.com/attachments/792473441390428170/823688284742877184/ffxiv_22032021_234231_957.png");
}
.controls{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 5px;
}
.player{
  display: flex;
  justify-content: center;
  align-items: center;
}
header {
  font-family: 'DotGothic16', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  margin-bottom: 5px;
  background-color: darkslateblue;
  color: white;
}
h2{
  padding: 3px;
  font-family: 'DotGothic16', sans-serif;
}
h3{
  font-family: 'DotGothic16', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top:10px;
  padding:5px;
}

.playlist{
  display: flex;
  flex-direction: column;
  align-items: center;

}

button{
  margin: 3px;
  padding: 3px;
}
</style>
