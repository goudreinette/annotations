<template>
  <div id="app" @mouseup="checkSelection" >
    <select-actions :show="showActions" :position="actionsPosition"></select-actions>
    <annotations :annotations="annotations"></annotations>

    <div class="textcontainer"  @mousedown="clearSelection">

    <div>
      non-selectable<br/>
      Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
    </div>
    <br/>

    <div class="selectable">
      Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
    </div>
  </div>

</div>
</template>

<script>
import SelectActions from './SelectActions.vue'
import Annotations from './Annotations.vue'

export default {
  components: {'select-actions': SelectActions, 'annotations': Annotations},
  data () {
    return {
      selection: '',
      actionsPosition: null,
      annotations: []
    }
  },
  methods: {
    checkSelection (e) {
      const selection = window.getSelection().toString()
      if (e.target.classList.contains('selectable') && selection  && selection !== ' ' && selection !== this.selection) {
        this.selection = selection
        if (e.target.getAttribute('id') !== 'select-actions')
          this.actionsPosition = [e.clientX, e.clientY]
      }
    },
    clearSelection () {
      window.getSelection().empty()
      this.selection = ''
    }
  },
    events: {
      'save-annotation': function () {
        this.annotations.push({text: this.selection, id: this.annotations.length})
      },
      'delete-annotation': function (id) {
        this.annotations.splice(this.annotations.indexOf(this.annotations.find(id)))
      },
      'clear-selection': function () {
        this.clearSelection()
      }
  },
  computed: {
    showActions () {
      return this.selection !== ''
    }
  }
}
</script>

<style>
html, body, #app {
  height: 100%;
  margin: 0;
  font-family: Cantarell;
}

.selectable::selection {
  background-color: rgba(135, 255, 0, 0.37);
}

</style>
