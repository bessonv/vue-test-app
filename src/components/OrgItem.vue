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
    console.log(this.organization && this.organization.id)
    if (this.organization) {
      this.itemId = this.organization.id
      this.organizationName = this.organization.orgName
      this.directorName = this.organization.dirName
      this.phone = this.organization.phone
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
