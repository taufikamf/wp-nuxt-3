<script setup>
const route = useRoute()
const { data: news } = await useFetch(`https://thedramaclubs.com/wp-json/wp/v2/posts?slug=${route.params.slug}`)
</script>
<template>
    <Head>
        <Title>Vercel App</Title>
        <Meta name="title" :content="news[0]?.yoast_head_json.og_title"/>
        <Meta name="description" :content="news[0]?.yoast_head_json.og_description"/>
        <Meta name="image" :content="news[0]?.yoast_head_json.og_image[0]?.url"/>
        <Meta name="og:title" :content="news[0]?.yoast_head_json.og_title"/>
        <Meta name="og:description" :content="news[0]?.yoast_head_json.og_description"/>
        <Meta name="og:image" :content="news[0]?.yoast_head_json.og_image[0]?.url"/>
    </Head>
    <p style="font-size: 0px;">{{ news[0]?.link }}</p>
</template>
<script>
export default{
    data(){
      return{
        domain: 'https://thedramaclubs.com/',
        slug: '',
        title: '',
        description: '',
        image: ''
      }
    },
    beforeCreate(){
        this.slug = this.$route.params.slug
        this.title = ''
        this.description = ''
        this.image = ''
    },
    async created() {
        // console.log(this.slug)
    // redirect to an external URL if the user came from Facebook
        this.slug = this.$route.params.slug
        if(this.slug == '/'){
            window.location.href = 'https://thedramaclubs.com/'
        }else if(this.slug != '/'){
            const slug = ref(this.slug)
            console.log(slug)
            const { data, pending, error, refresh } = await useLazyFetch('https://thedramaclubs.com/wp-json/wp/v2/posts',{
            query: { slug }
            })
            // console.log(data._rawValue[0].link)
            if(data){
                setTimeout(() => {
                    window.location.href = data._rawValue[0].link;
                }, 100);
                // window.location.href = data._rawValue[0].link
            }
        }
    }
}
</script>