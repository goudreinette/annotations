<template>
  <div id="select-actions" v-show="show" @click="clearSelection">
   <button @click="saveAnnotation">Save</button>
  </div>
</template>

<script>
import SelectActions from './SelectActions.vue'

export default {
  data () {
    return {

    }
  },
  props: ['show', 'position'],
  watch: {
    position (value) {
     const el = document.querySelector('#select-actions')
     el.style.left = `${value[0] - el.clientWidth / 2}px`
     el.style.top = `${value[1] - el.clientHeight - 20 }px`
    }
  },
  methods: {
    saveAnnotation() {
      console.log(this.$dispatch)
      this.$dispatch('save-annotation')
      this.$dispatch('clear-selection')
    },
    clearSelection() {
      this.$dispatch('clear-selection')
    }
  }
}
</script>

<style scoped>

#select-actions {
    position: fixed;
    background-color: rgba(0, 0, 0, 0.9);
    box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.5);
    border-radius: 10px;
    width: 200px;
    height: 50px;
    transition: opacity 1s;
}

button {
  width: 100%;
  background: none;
  border: none;
  color: white;
  height: 100%;
  font-weight: bold;
  font-family: Cantarell;
  font-size: 18px;
}

button:hover {
  -webkit-filter: brighten(10%);
  cursor: pointer;
}

</style>
