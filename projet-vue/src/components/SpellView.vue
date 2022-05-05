<template>
  <td>{{ spell[0] }}</td>
  <td>{{ spell[1] }}</td>
  <td>{{ spell[2] }}</td>
  <td>{{ spell[3].join(", ") }}</td>
  <td>{{ spell[4].map(e => e.join(': ')).join(', ') }}</td>
</template>

<script>
export default {
  name: 'SpellView',
  props: ['spell']
}
</script>

<style scoped>
</style>
