<template>
  <div id="app">
    <router-view />
    <FooterSection />
  </div>
</template>



<script>
import FooterSection from '@/components/FooterSection.vue'
export default {
  components: {
    FooterSection
  }

}
</script>
