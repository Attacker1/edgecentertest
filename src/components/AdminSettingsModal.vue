<template>
  <div class="admin-settings-modal__container">
    <base-modal ref="modal" :is-close-click-overlay="true">
      <form ref="saveForm" method="POST" name="saveForm" @submit.prevent="save">
        <div>
          <input class="panel-input" type="text" placeholder="Имя" v-model="name">
          <input class="panel-input" type="text" placeholder="Фамилия" v-model="surname">
          <input class="panel-input" type="text" placeholder="E-mail" v-model="email">
          <the-mask :mask="['+# (###) ###-##-##', '+## (###) ###-##-##']" v-model="phone"/>
          <textarea class="panel-input" placeholder="Сообщение" v-model="message"></textarea>
        </div>
        <div class="admin-settings-modal__actions">
          <a class="panel-btn panel-btn-accent" @click="save()">Сохранить</a>
          <a class="panel-btn" @click="close()">Отмена</a>
        </div>
      </form>
    </base-modal>
  </div>
</template>

<script>
import baseModal from './BaseModal.vue';
import { required, email, maxLength  } from '@vuelidate/validators'
import {TheMask} from 'vue-the-mask';

export default {
  name: "AdminSettingsModal",
  components: {
    baseModal,
    TheMask
  },
  data() {
    return {
      name: '',
      surname: '',
      phone: '',
      email: '',
      message: '',
      status: null
    }
  },
  methods: {
    save() {
      this.$refs.saveForm.$el.submit();
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.status = 'ERROR'
      } else {
        // Submit logic here
      }
    },
    close() {
      this.$emit('close');
    },
  },
  validations () {
    return {
      name: {
        required,
        maxLength: maxLength(100)
      },
      surname: {
        required,
        maxLength: maxLength(100)
      },
      email: {
        email: { required, email }
      },
      message: {
        required,
        maxLength: maxLength(500)
      },
    }
  }
}
</script>

<style>
.panel-btn {
  display: inline-block;
  line-height: 35px;
  background: #3b3b3b;
  color: #ffffff;
  border: none;
  border-radius: 20px;
  display: inline-block;
  outline: none !important;
  transition: opacity 200ms;
  vertical-align: top;
  font-size: 15px;
  font-weight: 400;
  text-align: center;
  padding: 0 20px;
  position: relative;
  cursor: pointer;
}

.panel-input {
  line-height: 38px;
  border: 1px solid #3f3f3f;
  font-size: 14px;
  width: 100%;
  max-width: 100%;
  outline: none;
  margin-bottom: 7px;
}
</style>