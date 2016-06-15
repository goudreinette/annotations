<template>
  <div id="annotations" :class="{'hide': hide}">

    <div class="annotation" v-for="annotation in annotations">
      {{annotation.text}}
    </div>

  </div>
</template>

<script>
import SelectActions from './SelectActions.vue'


export default {
  props: ['annotations'],
  data () {
    return {
      hide: true
    }
  },
  watch: {
    annotations (value) {
      this.hide = value.length <= 0
    }
  }
}
</script>

<style>

#annotations {
  position: fixed;
  right: 0;
  top: 0;
  height: 100%;
  width: 300px;
  background-color: lightgrey;
  border-left: 1px solid lightgrey;
  transition: all .5s ease-out;
  overflow: scroll;
}

#annotations::-webkit-scrollbar {
  display: none;
}

#annotations.hide {
  right: -300px;
}

.annotation {
  background-color: white;
  padding: 20px;
  border-bottom: 1px solid lightgrey;
}

</style>
