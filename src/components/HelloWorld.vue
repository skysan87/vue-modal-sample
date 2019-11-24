<template>
  <div class="hello">
    <input type="text" name="message" v-model="message">
    <div>
      <button @click="isModal = true">Show Dialog</button>
    </div>

    <ModalDialog v-if="isModal"
      @close="update"
      v-bind:comment="message"
      ></ModalDialog>
  </div>
</template>

<script>
import ModalDialog from './ModalDialog.vue'

export default {
  name: 'HelloWorld',
  components: {
    ModalDialog
  },
  data() {
    return {
      isModal: false,
      message: ""
    }
  },
  methods: {
    update: function(comment) {
      this.message = comment
      this.isModal = false
    }
  }
}
</script>
