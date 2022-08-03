<template>
  <OrgItem />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import OrgItem from './OrgItem.vue'

export default defineComponent({
  name: 'OrgTable',
  components: {
    OrgItem
  },
  props: {
    list: []
  }
})
</script>

<style lang="scss">

</style>
