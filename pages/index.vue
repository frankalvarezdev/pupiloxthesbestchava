<template>
    <div>
        <div class='home'>
            <div class='home-c-img'>
                <svg
                    class='portada'
                    version='1.1'
                    xmlns='http://www.w3.org/2000/svg'
                    xmlns:xlink='http://www.w3.org/1999/xlink'
                    preserveAspectRatio='xMidYMid meet'
                    viewBox='-204.63833333333235 -40.999999999999886 1284.0000000000002 723.9999999999999'
                    width='100%'
                    :style='`background-image: url("/cdn/img/team/team.jpg"); animation: none;`'
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
            <div class='description'>
                <div>
                    <h1 class='home-title'>Pupilo X Thes Best Chava</h1>
                    <span
                        class='home-desc'
                    >Somos dos adolescentes amantes de los viajes y bromas. Para nosotros lo importante siempre sera sacarles una sonrisa!</span>
                </div>
            </div>
        </div>
        <section class='home-section'>
            <div class='team' id='team'>
                <div v-for='member of team' :key='member.slug'>
                    <nuxt-link :to='`/team/${member.slug}`'>
                        <div class='team-img' :style='`--team-img: url(${member.img})`'>
                            <svg
                                class='team-svg'
                                width='100%'
                                height='100%'
                                viewBox='0 0 960 1280'
                                version='1.1'
                                xmlns='http://www.w3.org/2000/svg'
                                xmlns:xlink='http://www.w3.org/1999/xlink'
                                xml:space='preserve'
                                xmlns:serif='http://www.serif.com/'
                            >
                                <rect x='0' y='0' width='960' height='1280' />
                            </svg>
                            <span class='title'>{{getTeamData(member.name)}}</span>
                        </div>
                    </nuxt-link>
                </div>
            </div>
            <h1 class='videos-title'>ULTIMOS VIDEOS</h1>
            <div class='videos'>
                <div class='video' v-for='(n, index) in 8' :key='index'>
                    <a :href='getVideoLink(n)' target='_blank'>
                        <svg
                            class='youtube-video-img'
                            version='1.1'
                            xmlns='http://www.w3.org/2000/svg'
                            xmlns:xlink='http://www.w3.org/1999/xlink'
                            preserveAspectRatio='xMidYMid meet'
                            viewBox='-204.63833333333235 -40.999999999999886 1284.0000000000002 723.9999999999999'
                            width='100%'
                            :style='`background-image: url(${getYtId(n)}); animation: none;`'
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
                    </a>
                    <span class='video-title' v-html='getVideoTitle(n)'></span>...
                    <a :href='getVideoLink(n)' target='_blank'>
                        <i class='fas fa-play-circle'></i> Ver video
                    </a>
                </div>
            </div>
        </section>
    </div>
</template>
<script>
import axios from "axios";
export default {
    mounted() {
        this.getData();
    },
    data() {
        return {
            videos: [],
        };
    },
    async asyncData({ $content, params }) {
        const team = await $content("team", params.slug)
            .only(["name", "img", "slug"])
            .sortBy("createdAt", "asc")
            .fetch();

        return {
            team,
        };
    },
    methods: {
        getData() {
            axios
                .get(
                    "https://api.rss2json.com/v1/api.json?rss_url=https://www.youtube.com/feeds/videos.xml?channel_id=UCoG6kpIgPKdsMfoDqrSmcEw"
                )
                .then((response) => {
                    this.videos = response.data.items;
                });
        },
        getYtId: function (myString) {
            if (this.videos.length > 0) {
                var myString = this.videos[myString].guid;
                return (
                    "https://img.youtube.com/vi/" +
                    myString.split(":")[2] +
                    "/maxresdefault.jpg"
                );
            }
        },
        getVideoTitle(n) {
            if (this.videos.length > 0) {
                return this.videos[n].title.slice(0, 50);
            }
        },
        getVideoLink(n) {
            if (this.videos.length > 0) {
                return this.videos[n].link;
            }
        },
        getTeamData(data) {
            data = data.split(" ");
            return `${data[0]} ${data[1]}`;
        },
    },
    head() {
        return {
            title: "PUPILO X THES BEST CHAVA",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Sitio oficial de  PUPILO X THES BEST CHAVA",
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
@import "~/assets/pages/index.scss";
</style>