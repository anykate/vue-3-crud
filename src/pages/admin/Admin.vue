<template>
  <div class="container">
    <div class="row">
      <div class="col-md-3 ps-0">
        <Sidebar />
      </div>
      <div class="col-md-9 pe-0">
        <router-view />
      </div>
    </div>
  </div>
</template>

<script>
import Sidebar from '@/components/Sidebar'

export default {
  name: "Admin",
  components: {
    Sidebar
  }
}
</script>

<style scoped>
</style>