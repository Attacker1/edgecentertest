<template>
  <div>
    <div class="vue-base-modal-overlay" @click="close(true)"></div>
    <div class="vue-base-modal">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "BaseModal",
  components: {
  },
  props: {
    isCloseClickOverlay: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isOpen: false
    }
  },
  methods: {
    open() {
      this.isOpen = true;
    },
    close(isOverlay = false) {
      if(!isOverlay || (isOverlay && this.isCloseClickOverlay))
        this.isOpen = false;
    }
  },
}
</script>

<style>
.vue-base-modal-overlay{
  position: fixed;
  background: #000;
  opacity: .75;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 10000;
}
.vue-base-modal{
  position: fixed;
  background: #1a1a1a;
  width: 450px;
  padding: 45px 35px;
  left: calc(50% - 225px);
  top: 100px;
  z-index: 10001;
}

@media (max-width: 560px) {
  .vue-base-modal {
    width: calc(100vw - 20px);
    left: 10px;
    top: calc(50vh - 45px);
    padding: 10px;
  }
}
</style>