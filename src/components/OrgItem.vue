<template>
  <div></div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'OrgItem',
  props: {
    organizationName: String,
    directorName: String,
    phone: Number
  }
})
</script>

<style lang="scss">

</style>
