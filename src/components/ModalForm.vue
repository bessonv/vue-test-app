<template>
  <div class="backdrop">
    <div class="modal">
      <h2>Добавить организацию</h2>
      <form>
        <label>Название:</label>
        <input type="text" required v-model="orgName" @keyup="isDataFilled">

        <label>Номер телефона:</label>
        <input type="text" required v-model="phone" @keyup="isDataFilled">
        <div class="warning" v-if="warning">Неверный формат номера телефона</div>

        <label>ФИО директора</label>
        <input type="text" :class="{ warn: warning && !dirName }" required v-model="dirName" @keyup="isDataFilled">
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
      this.$emit('close')
    },
    saveForm () {
      if (this.isDataFilled()) {
        if (Number(this.phone) && this.phone.length >= 6) {
          this.$emit('save', { orgName: this.orgName, phone: this.phone, dirName: this.dirName })
        } else {
          this.warning = true
        }
      }
    },
    isDataFilled () {
      if (this.orgName && this.phone && this.dirName) {
        this.isDisabled = false
        return true
      } else {
        this.isDisabled = true
        return false
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
      background: rgba(0,0,0,0.3);
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
        margin: 20px auto;
        text-align: left;
        padding: 0 40px 20px 40px;
      }

      label {
        display: inline-block;
        margin: 35px 0 10px;
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
        cursor: pointer;
        color: #333;
        padding: 8px;
        border: 1px solid #eee;
        border-radius: 4px;
        margin: 10px;
        min-width: 70px;

        &:disabled {
          cursor: default;
        }
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
