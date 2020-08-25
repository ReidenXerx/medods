<template v-on:event-length="checkLength" lang="html">
<div class="">
  <p>{{ msg }}</p>
  <div class="container">
    <Sector v-for="numberSector in 4" :id="numberSector" :blink="blinkArray[numberSector - 1]"
    @click="handlerSectorclick(numberSector)"/>
  </div>
  <button type="button" @click="demonstratePhase" name="start">start</button>
</div>

</template>

<script>
import Sector from "@/components/Sector.vue"
export default {
  components: {
    Sector
  },
  props: {
    msg: {
       type: String,
       required: true,
       default: 'Tom',
       validator: function(value){
           return value!='admin' && value!='';
       }
     }
  },
  data() {
    return {
      blinkArray: [
        false, false, false, false
      ],
      blinkQuery: [],
      blinkQueryUser: [],
      blinkCount: 3,
      playing: false
    }
  },
  methods : {
    generateQuery: function() {
      for (var i = 0; i < this.blinkCount; i++) {
        this.blinkQuery.push(this.getRandomInt(3) + 1)
      }
    },

    clearQuery: function() {
      this.blinkQuery.splice(0, this.blinkQuery.length)
    },

    handlerBlink: function(actions) {
      this.blinkQuery.forEach((item, i) => {
        //this.blinkArray[item] = true // не работает
        this.$set(this.blinkArray, item, true)
        actions(item)
      })
    },

    clearQuery: function() {
      this.blinkQuery.splice(0, this.blinkQuery.length)
    },

    handlerBlink: function() {
      let indexer = 0
      console.log(`query ${this.blinkQuery}`);
      const interval = setInterval(() => {//0
        this.$set(this.blinkArray, this.blinkQuery[indexer], true) //свечение
        console.log('light on ' + indexer + ' iterations');
        this.waitBlink().then(() => {

          this.$set(this.blinkArray, this.blinkQuery[indexer], false) // погасание
          console.log('light off ' + indexer + ' iterations');
          indexer++
          if (indexer == this.blinkCount) {
            clearInterval(interval)
            console.log('interval cleared');
          }
        })
      }, 2200)
    },

    demonstratePhase: function() {
      window.alert('demonstrate')
      this.generateQuery()
      this.handlerBlink()
      this.playing = true
    },

    checkPhase: function() {
        this.playing = true

        this.listen((bool) => {// вернуть тру или фолс
          return bool
      })
    },

    listen: function() {
      return new Promise((resolve) => {

        do {
          if (state == 1) { // стек идентичен
            resolve(true)
          }
        } while (state == 0)
      })
    },

    handlerSectorclick: function(index) {
      console.log('handler sector')
      if (index == this.blinkQuery[this.blinkQueryUser.length + 1] &&
          this.blinkQueryUser.length <= this.blinkQuery.length - 1 && this.playing) {

        this.blinkQueryUser.push(index)
      }
      else if (index != this.blinkQuery[this.blinkQueryUser.length + 1]) {
        window.alert('you are debil')
        return
      }
      else if (this.blinkQueryUser === this.blinkQuery) {
        window.alert('you are NOT debil')
        this.blinkCount++
        this.demonstratePhase()
      }
    },

    // handlerBlink: function(actions) {
    //   let indexer = 0
    //   const interval = setInterval(() => {
    //     this.$set(this.blinkArray, this.blinkQuery[indexer], true)
    //
    //     actions(this.blinkQuery[indexer])
    //     indexer++
    //     if (indexer == this.blinkCount) {
    //       clearInterval(interval)
    //     }
    //   }, 2200)
    // },
    //
    // timelineMain: function() {
    //   this.generateQuery()
    //
    //   this.handlerBlink((item) => {
    //
    //     this.waitBlink().then(() => {
    //
    //       this.$set(this.blinkArray, item, false)
    //     })
    //   })
    // },

    waitBlink: function() {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve()
        }, 2000)
      })
    },

    // utilities
    getRandomInt: function(max) {
      return Math.floor(Math.random() * Math.floor(max))
    }
  }
}
</script>

<style lang="scss" scoped>
  .container {
    display: flex;
    width: 400px;
    flex-wrap: wrap;
  }
</style>
