<template lang="html">
  <!-- <div class="item" v-bind:class="{ 'item-1': id == 0, 'item-2': id == 1, 'item-3': id == 2, 'item-4': id == 3}"></div> -->
  <div class="item" v-bind:class="[{ 'whiter': blink }, classObject.result]"><p>{{blink}}</p></div>
  <!-- <p>{{classObject}}</p> -->
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      default: 0
    },
    blink: {
      type: Boolean
    }
  },
  data() {
    return {
      a: 0
    }
  },
  computed: {
    classObject:function() {
      return {
        result: `item-${this.id}`
      }
    }
  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
  .item {
    width: 200px;
    height: 200px;
    border: 1px black;
  }

  .item-1 {
    border-radius: 100% 0 0 0;
    background-color: blue;
  }

  .item-2 {
    border-radius: 0 100% 0 0;
    background-color: black;
  }

  .item-3 {
    border-radius: 0 0 0 100%;
    background-color: green;
  }

  .item-4 {
    border-radius: 0 0 100% 0;
    background-color: red;
  }

  .whiter {
    opacity: 20%;
  }
</style>
