<template>
  <td>{{ organizationName }}</td>
  <td>{{ directorName }}</td>
  <td>{{ phone }}</td>
  <td class="remove-button" @click="removeItem">x</td>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import { orgType } from '../types'

export default defineComponent({
  name: 'OrgItem',
  props: {
    organization: Object as PropType<orgType>
  },
  methods: {
    removeItem () {
      this.$emit('remove', this.itemId)
    }
  },
  data () {
    return {
      itemId: 0,
      organizationName: '',
      directorName: '',
      phone: ''
    }
  },
  mounted () {
    if (this.organization) {
      this.itemId = this.organization.id
      this.organizationName = this.organization.orgName
      this.directorName = this.organization.dirName
      const mobile = this.organization.phone.match(/^(\d{1})(\d{3})(\d{3})(\d{2})(\d{2})$/)
      const home = this.organization.phone.match(/^(\d{2})(\d{2})(\d{2})$/)
      const phone = mobile || home
      if (phone) {
        phone.shift()
        this.phone = phone.join('-')
      } else {
        this.phone = this.organization.phone
      }
    }
  }
})
</script>

<style lang="scss">
.remove-button {
  cursor: pointer;
  background-color: crimson;
}
</style>
