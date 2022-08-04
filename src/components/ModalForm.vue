<template>
  <div class="backdrop">
    <div class="modal">
      <h2>Добавить организацию</h2>
      <form>
        <label>Название:</label>
        <input type="text" :class="{ warn: warning && !orgName }" required v-model="orgName" @keyup="isDataFilled">
        <div class="warning" v-if="warning && !orgName">Пустое поле</div>

        <label>Номер телефона:</label>
        <input type="text" :class="{ warn: warning && !phone }" required v-model="phone" @keyup="isDataFilled">
        <div class="warning" v-if="warning && !phone">Пустое поле</div>

        <label>ФИО директора</label>
        <input type="text" :class="{ warn: warning && !dirName }" required v-model="dirName" @keyup="isDataFilled">
        <div class="warning" v-if="warning && !dirName">Пустое поле</div>
      </form>
      <button @click="closeModal">Отмена</button>
      <button @click="saveForm" :disabled="isDisabled">Ок</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ModalForm',
  data () {
    return {
      orgName: '',
      phone: '',
      dirName: '',
      isDisabled: true,
      warning: false
    }
  },
  methods: {
    closeModal () {
      console.log('close')
      this.$emit('close')
    },
    saveForm () {
      // if (this.isDataFilled()) {
      this.$emit('save', { orgName: this.orgName, phone: this.phone, dirName: this.dirName })
      // } else {
      //   this.warning = true
      // }
    },
    isDataFilled () {
      if (this.orgName && this.phone && this.dirName) {
        this.isDisabled = false
        return false
      } else {
        this.isDisabled = true
        return true
      }
    }
  }
})
</script>

<style lang="scss">
  .backdrop {
      top: 0;
      left: 0;
      position: fixed;
      background: rgba(0,0,0,0.5);
      width: 100%;
      height: 100%;
  }
  .modal {
      width: 400px;
      padding: 20px;
      margin: 100px auto;
      background: white;
      border-radius: 10px;

      form {
        margin: 30px auto;
        text-align: left;
        padding: 40px;
      }

      label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        font-weight: bold;
      }

      input {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        color: #555;

        &.warn {
          border: 2px solid crimson;
        }
      }

      button {
          color: #333;
          padding: 8px;
          border: 1px solid #eee;
          border-radius: 4px;
          text-decoration: none;
          margin: 10px;
      }

      .warning {
        font-size: 0.8em;
        color: crimson;
      }

      h1 {
          color: #03cfb4;
      }

      p {
          font-style: normal;
      }
  }
</style>
