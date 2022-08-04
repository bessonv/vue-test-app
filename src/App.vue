<template>
  <main>
    <div class="container">
      <input type="text" v-model="searchText" @keyup="handleTextChange">
      <button @click="toggleModal">Добавить</button>
    </div>
    <OrgTable :orgList="orgList" @removeItem="removeItem"/>
    <div v-if="showModal">
      <ModalForm @close="toggleModal" @save="addOrganization"/>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import ModalForm from './components/ModalForm.vue'
import OrgTable from './components/OrgTable.vue'
import data from './mockData'
import { orgType } from './types'

const orgData = data

export default defineComponent({
  name: 'App',
  data () {
    return {
      orgList: orgData,
      searchText: '',
      showModal: false
    }
  },
  components: {
    ModalForm,
    OrgTable
  },
  methods: {
    removeItem (id: number) {
      this.orgList = this.orgList.filter(item => item.id !== id)
      console.log(this.orgList)
    },
    handleTextChange (e: Event) {
      const searchText = e.target && e.target.value.toLowerCase()
      this.orgList = orgData.filter(item => item.dirName.toLowerCase().includes(searchText))
    },
    toggleModal () {
      this.showModal = !this.showModal
    },
    addOrganization (data: { orgName: string, phone: string, dirName: string }) {
      const { orgName, phone, dirName } = data
      const newOrganization: orgType = {
        id: orgData.length + 1,
        orgName,
        phone,
        dirName
      }
      orgData.push(newOrganization)
      this.orgList = orgData
      this.showModal = false
    }
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

  .container {
    input {
      text-align: left;
      display: inline-block;
      padding: 5px 5px;
      box-sizing: border-box;
      color: #555;
    }

    button {
      text-align: right;
      color: #333;
      cursor: pointer;
      padding: 6px 8px;
      border: 1px solid #e9e9e9;
      border-radius: 4px;
      text-decoration: none;
      margin: 10px;
    }
  }
}
</style>
