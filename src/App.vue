<template>
  <OrgTable />
  <ModalForm />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import ModalForm from './components/ModalForm.vue'
import OrgTable from './components/OrgTable.vue'

export default defineComponent({
  name: 'App',
  components: {
    ModalForm,
    OrgTable
  }
})
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
