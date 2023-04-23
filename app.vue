<template>
  <div>
    <section v-if="showContent">
      <NuxtWelcome/>
    </section>
    <section v-else>
      <NuxtLayout>
        <NuxtPage/>
      </NuxtLayout>
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
        if(!referrer.includes('facebook')){
          return true
        }else{
          return false
        }
      }
    }
  },
}
</script>
