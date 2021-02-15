<template>
    <div class='main-blog'>
        <h1>Publicaciones del blog</h1>
        <div class='blog-posts'>
            <div v-for='article of articles' :key='article.slug'>
                <NuxtLink class="nuxt-llink" :to='{ name: "blog-slug", params: { slug: article.slug } }'>
                    <svg
                        class='article-img'
                        version='1.1'
                        xmlns='http://www.w3.org/2000/svg'
                        xmlns:xlink='http://www.w3.org/1999/xlink'
                        preserveAspectRatio='xMidYMid meet'
                        viewBox='-204.63833333333235 -40.999999999999886 1284.0000000000002 723.9999999999999'
                        width='100%'
                        :style='`background-image: url(${article.img}); animation: none;`'
                    >
                        <defs>
                            <path
                                d='M-203.64 -40L1076.36 -40L1076.36 680L-203.64 680L-203.64 -40Z'
                                id='cSO6LWgP4'
                            />
                        </defs>
                        <g>
                            <use xlink:href='#cSO6LWgP4' opacity='1' fill-opacity='1' />
                        </g>
                    </svg>
                    <div>
                        <h2 class='article-title'>{{ article.title }}</h2>
                        <span class='article-desc'>{{ article.description }}</span>
                    </div>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    async asyncData({ $content, params }) {
        let articles = await $content("articles", params.slug)
            .only(["title", "description", "img", "slug"])
            .sortBy("createdAt", "asc")
            .fetch();
        return {
            articles
        };
    },
    head() {
        return {
            title: "BLOG - PUPILO X THES BEST CHAVA",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Blog de  PUPILO X THES BEST CHAVA",
                },
                {
                    property: "og:image",
                    content:
                        "https://pupiloxthesbestchava.netlify.app/cdn/img/team/team.jpg",
                },
                { name: "twitter:card", content: "summary" },
                // { name: "twitter:site", content: "@xpendmusic" },
                {
                    name: "twitter:image",
                    content:
                        "https://pupiloxthesbestchava.netlify.app/cdn/img/team/team.jpg",
                },
            ],
        };
    },
};
</script>
<style lang="scss" scoped>
@import "~/assets/pages/blog/index.scss";
</style>