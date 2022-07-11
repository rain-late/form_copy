<template>
  <div>{{ defaultValue }}</div>
</template>
<script>
export default {
  props: {
    defaultValue: {
      type: String,
      default: ''
    }
  },
  data() {
    return {}
  }
}
</script>
