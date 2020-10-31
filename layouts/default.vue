<template>
  <div>
    <div>
      <header-component />
      <Nuxt />
    </div>
  </div>
</template>

<style>

</style>
<script>
import HeaderComponent from '~/components/layouts/header-component'
export default {
  components: { HeaderComponent }
}
</script>
