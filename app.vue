<template>
  <div>
    <section v-if="showContent">
      <NuxtWelcome/>
    </section>
  </div>
</template>

<script>
export default {
  computed: {
    showContent() {
      // check if the user came from Facebook
      if (typeof document !== 'undefined') {
      const referrer = document.referrer.toLowerCase()
      return !referrer.includes('facebook')
      }
    }
  },
  mounted() {
    // redirect to an external URL if the user came from Facebook
    const referrer = document.referrer.toLowerCase()
    if (referrer.includes('facebook')) {
      window.location.replace('https://thedramaclubs.com/')
    }
  }
}
</script>
