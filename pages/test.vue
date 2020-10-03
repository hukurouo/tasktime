<template>
  <section class="section">
    <div class="columns is-mobile">
      <card
        title="Free"
        icon="github"
      >
        Open source on <a href="https://github.com/buefy/buefy">
          GitHub
        </a>
      </card>
    </div>
    <div>
      {{ sec }}
      <br>
      {{ formatTime }}
       <b-button @click="start" v-if="!timerOn">start</b-button>
       <b-button @click="stop" v-if="timerOn">stop</b-button>
    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'

export default {
  name: 'HomePage',
  data () {
    return {
      sec: 0,
      timerOn: false,
      timerObj: null,
    }
  },
  methods: {
    count: function() {
      this.sec = this.sec + 1
    },

    start: function() {
      let self = this;
      this.timerObj = setInterval(function() {self.count()}, 1000)
      this.timerOn = true; 
    },

    stop: function() {
      clearInterval(this.timerObj);
      this.timerOn = false; 
    },
  },
  computed: {
    formatTime: function() {
      var rawsec = this.sec
      var sec = String((rawsec % 60)%60)
      if (sec.length == 1){sec = "0" + sec}
      var min = String(Math.floor(rawsec / 60) % 60)
      if (min.length == 1){min = "0" + min}
      var hour = String(Math.floor(rawsec / 3600))
      if (hour.length == 1){hour = "0" + hour}
      var time = hour + ":" + min + ":" + sec
      return time
    },
  },

  components: {
    Card
  }
}



</script>
