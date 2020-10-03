<template>
  <section class="container">
    <b-message auto-close duration="3000" v-model="isActive" aria-close-label="Close message">
        タスクを追加しました
    </b-message>
    
    <div v-if="set_task">
      {{ set_task_name }} : {{ formatTime }}
      <br><br>
       <b-button @click="start" v-if="!timerOn">start</b-button>
       <b-button @click="stop" v-if="timerOn">stop</b-button>
       <hr>
    </div>

    <div>
      <b-button @click="addTask">タスクを追加</b-button>
    </div>
    <br>
    
    <div v-for="(task) in tasks" :key="task.id">
      <card
        :title=task.name
        :formatsec=task.sec
        :totalsec=task.total_sec
      >
      <a class="card-footer-item" @click="setTask(task.name)">Set</a>
      <a class="card-footer-item">Edit</a>
      <a class="card-footer-item">Done</a>
      <a class="card-footer-item">Delete</a>
      </card>
      <br>
    </div>
    
  </section>
</template>

<style>
.container {
  padding: 20px;
}

</style>

<script>
import Card from '~/components/Card'

export default {
  name: 'HomePage',
  data () {
    return {
      tasks: {
        "task1":{
          "sec": 0,
          "total_sec": 19,
          "name":"task1",
        }, 
        "task2":{
          "sec": 0,
          "total_sec": 5,
          "name":"task2",
        },
      },
      sec: 0,
      hoge: {},
      set_task_name: "",
      isActive: false,
      set_task: false,
      timerOn: false,
      timerObj: null,
    }
  },
  methods: {
    count: function() {
      this.sec = this.sec + 1
    },

    start: function() {
      var self = this;
      this.timerObj = setInterval(function() {self.count()}, 1000)
      this.timerOn = true; 
    },

    stop: function() {
      this.tasks[this.set_task_name].total_sec += this.sec
      this.sec = 0
      clearInterval(this.timerObj);
      this.timerOn = false; 
    },

    setTask: function(name) {
      this.set_task_name = name
      this.set_task = true
    },
    
    addTask: function(){
      this.tasks["task3"] = {
          "sec": 0,
          "total_sec": 0,
          "name":"task3",
        }
      this.isActive = true
    }

  },
  computed: {
    formatTime: function() {
      return this.SecToTime(this.sec)
    },
  },

  components: {
    Card
  }
}



</script>
