<template>
  <main>
    <div class="container">
      <input type="text" placeholder="Найти по ФИО" v-model="searchText" @keyup="handleTextChange">
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
    },
    handleTextChange (e: Event) {
      const searchText = (e.target as HTMLInputElement).value
      if (searchText) {
        this.orgList = orgData.filter(item => item.dirName.toLowerCase().includes(searchText))
      } else {
        this.orgList = orgData
      }
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
      this.orgList.push(newOrganization)
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
    margin: 0 auto;
    padding: 0 40px;
    max-width: 800px;
    display: flex;
    justify-content: space-between;

    input {
      padding: 5px 5px;
      box-sizing: border-box;
      color: #555;
    }

    button {
      color: #333;
      cursor: pointer;
      padding: 6px 8px;
      border: 1px solid #e9e9e9;
      border-radius: 4px;
    }
  }
}
</style>
