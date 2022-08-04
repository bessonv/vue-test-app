<template>
  <OrgTable :orgList="orgList"/>
  <ModalForm />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import ModalForm from './components/ModalForm.vue'
import OrgTable from './components/OrgTable.vue'
import data from './mockData'

export default defineComponent({
  name: 'App',
  data () {
    return {
      orgList: data
    }
  },
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
