<template>
    <p>{{ $route.params.slug }}</p>
    <p>{{ data }}</p>
</template>
<script>
export default{
    data(){
      return{
        domain: 'https://thedramaclubs.com/',
        data: {},
        slug: '',
      }
    },
    beforeMount(){
        this.slug = this.$route.params.slug
    },
    async mounted() {
    // redirect to an external URL if the user came from Facebook
        const referrer = document.referrer.toLowerCase()
        if(this.slug == '/'){
            window.location.href = 'https://thedramaclubs.com/'
        }else if(this.slug != '/'){
            const slug = ref(this.slug)
            const { data, pending, error, refresh } = await useFetch('https://thedramaclubs.com/wp-json/wp/v2/posts',{
            query: { slug }
            })
            this.data == data
            // window.location.href = data.value[0].link
        }
    }
}
</script>