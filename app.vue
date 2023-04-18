<template>
  <div>
    <section v-if="showContent">
      <NuxtWelcome/>
    </section>
  </div>
</template>

<script>
export default {
  data(){
    return{
      domain: 'https://thedramaclubs.com/',
      data: {},
      slug: '',
      link: ''
    }
  },
  async created(){
    
  },  
  computed: {
    showContent() {
      // check if the user came from Facebook
      if (typeof document !== 'undefined') {
      const referrer = document.referrer.toLowerCase()
      return !referrer.includes('facebook')
      }
    }
  },
  async mounted() {
    // redirect to an external URL if the user came from Facebook
    const referrer = document.referrer.toLowerCase()
    if (referrer.includes('facebook')) {
      if(this.slug == '/'){
        window.location.href = 'https://thedramaclubs.com/'
      }else if(this.slug != '/'){
        this.slug = this.$route.path
        const slug = ref(this.slug)
        const { data, pending, error, refresh } = await useFetch('https://thedramaclubs.com/wp-json/wp/v2/posts',{
          query: { slug }
        })
        window.location.href = data.value[0].link
      }
    }
  }
}
</script>
