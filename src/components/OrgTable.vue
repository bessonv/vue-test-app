<template>
<div class="wrapper" v-if="showTable">
  <table class="table">
    <tr class="row-header">
      <th v-for="header in headers" :key="header.type" @click="toggleSort($event, header.type)">
        {{ header.name }}
        <span v-if="sortType === header.type && sortAsc">↓</span>
        <span v-if="sortType === header.type && !sortAsc">↑</span>
      </th>
      <th></th>
    </tr>
    <tr v-for="org in onPage" :key="org.id">
      <OrgItem
        :organization="org"
        @remove="removeOrg" />
    </tr>
  </table>
  <div class="table-pagination">
    <button @click="prevPage">←</button>
    <div>Страница {{ page }}</div>
    <button @click="nextPage">→</button>
  </div>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import OrgItem from './OrgItem.vue'
import { orgType, orgHeader } from '../types'

export default defineComponent({
  name: 'OrgTable',
  components: {
    OrgItem
  },
  props: {
    orgList: {
      type: Array as () => orgType[],
      required: true
    },
    elementsOnPage: {
      type: Number,
      required: false,
      default: 5
    }
  },
  data () {
    return {
      list: [] as orgType[],
      headers: [
        { name: 'Название', type: 'orgName' },
        { name: 'ФИО директора', type: 'dirName' },
        { name: 'Номер телефона', type: 'phone' }] as orgHeader[],
      sortAsc: false,
      sortType: '',
      showTable: true,
      page: 1
    }
  },
  mounted () {
    this.list = this.orgList
  },
  updated () {
    this.list = this.orgList
  },
  methods: {
    prevPage () {
      if (this.page > 1) {
        this.page--
      }
    },
    nextPage () {
      if (this.page <= Math.floor(this.list.length / this.elementsOnPage)) {
        this.page++
      }
    },
    sort (fEl: orgType, sEl: orgType) {
      const type = this.sortType as keyof orgType
      if (Object.prototype.hasOwnProperty.call(fEl, type)) {
        const fa = fEl[type]
        const fb = sEl[type]
        const ascMult = ((this.sortAsc) ? 1 : -1)
        if (fa < fb) {
          return -1 * ascMult
        }
        if (fa > fb) {
          return 1 * ascMult
        }
        return 0
      }
      return 0
    },
    toggleSort (e: Event, sortType: string) {
      this.sortType = sortType
      this.sortAsc = !this.sortAsc
      this.list.sort(this.sort)
    },
    removeOrg (id: number) {
      this.$emit('removeItem', id)
    }
  },
  computed: {
    onPage () {
      return this.list.slice((this.page - 1) * this.elementsOnPage, this.page * this.elementsOnPage)
    }
  }
})
</script>

<style lang="scss">
.wrapper {
  margin: 0 auto;
  padding: 10px 40px;
  max-width: 800px;

  .table {
    margin: 0 0 40px 0;
    width: 100%;
    display: table;

    tr {
      display: table-row;
      background: #f6f6f6;

      &:nth-of-type(odd) {
        background: #e9e9e9;
      }

      &.row-header {
        th {
          cursor: pointer;
          padding: 6px 12px;
          font-weight: 900;
          color: #ffffff;
          background: #6c7a89;
          border-radius: 4px;
        }
      }

      td {
        padding: 6px 12px;
        display: table-cell;
      }
    }
  }

  .table-pagination {
    button, div {
      display: inline;
    }

    button {
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
