<template>
    <article class='article-main'>
        <div class='article-header'>
            <div class='article-title'>
                <div>
                    <h1 class="h-title">{{ article.title }}</h1>
                    <p>{{ formatDate(article.updatedAt) }}</p>
                </div>
            </div>
            <div>
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
            </div>
        </div>
        <nuxt-content class="blog-content" :document='article' />
    </article>
</template>
<script>
export default {
    async asyncData({ $content, params }) {
        const article = await $content("articles", params.slug).fetch();

        return { article };
    },
    methods: {
        formatDate(date) {
            const options = { year: "numeric", month: "long", day: "numeric" };
            return new Date(date).toLocaleDateString("es", options);
        },
    },
    head() {
        return {
            title: this.article.title + " - PUPILO X THES BEST CHAVA",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: this.article.description,
                },
                { property: "og:image", content: `/cdn/img/blog/${this.article.img}` },
                { name: "twitter:card", content: "summary" },
                // { name: "twitter:site", content: "@xpendmusic" },
                { name: "twitter:image", content: `/cdn/img/blog/${this.article.img}` },
            ],
        };
    },
};
</script>
<style lang="scss">
@import "~/assets/pages/blog/slug.scss";
</style>