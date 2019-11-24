<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <!-- フォーカスアウト防止 -->
          <div tabindex="0" class="dummy"></div>

          <div class="modal-body">
            <input class="input-text" type="text" v-model="inputtext" ref="modalcomment" />
          </div>

          <div class="modal-footer">
            <button class="btn-regular modal-default-button" @click="update">OK</button>
            <button class="btn-gray modal-default-button" @click="cancel">キャンセル</button>
          </div>

          <!-- フォーカスアウト防止 -->
          <div tabindex="0" class="dummy"></div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalDialog",
  props: {
    comment: String
  },
  data() {
    return {
      inputtext: this.comment
    };
  },
  methods: {
    update: function() {
      this.$emit("close", this.inputtext);
    },
    cancel: function() {
      this.$emit("close", this.comment);
    },
    checkFocus: function(ev) {
      if (ev.target !== null && ev.target.className == "dummy") {
        this.$refs.modalcomment.focus();
      }
    }
  },
  created() {
    document.addEventListener("focusin", this.checkFocus, false);
  },
  mounted() {
    this.$refs.modalcomment.focus();
  },
  beforeDestroy() {
    document.removeEventListener("focusin", this.checkFocus, false);
  }
};
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.1s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  min-height: 100px;
  margin: 30px auto 0;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-body {
  margin: 10px 0;
}

.modal-footer {
  margin: 5px 0;
  height: 20px;
}

.input-text {
  width: 100%;
  line-height: 1.5;
}

.modal-default-button {
  margin-left: 10px;
  float: right;
}

.status-labels {
  display: flex;
  justify-content: space-evenly;
}

/* transition="modal"に適用される */
.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>