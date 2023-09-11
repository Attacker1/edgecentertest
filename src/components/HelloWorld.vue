<template>
  <div class="hello">
    <h1>Снизу кнопка для открытия модалки</h1>
    <button id="show-modal" @click="isOpen = true">Show Modal</button>
    <AdminSettingsModal
        v-if="isOpen" @close="isOpen = false"
    />
  </div>
</template>

<script>
import AdminSettingsModal from "@/components/AdminSettingsModal.vue";

export default {
  name: 'HelloWorld',
  components: {
    AdminSettingsModal
  },
  data() {
    return {
      isOpen: false
    }
  },
  setup() {
  }
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
