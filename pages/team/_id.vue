<template>
    <div>
        <div class='member-header'>
            <div class='member-header__left'>
                <svg
                    xmlns='http://www.w3.org/2000/svg'
                    viewBox='0 0 24 24'
                    :style='`background-image: url("/cdn/img/team/${member.id}.jpg")`'
                    class='member-svg'
                >
                    <path d='M24 0h-24v24h24v-24z' />
                </svg>
            </div>
            <div class='member-header__right'>
                <div>
                    <span class='member-header__country'>
                        <i class='fas fa-map-marker-alt'></i>
                        {{member.country}} • 
                        <i class='fas fa-birthday-cake'></i>
                        {{member.date}}
                    </span>
                    <h1 class='member-header__title'>{{member.name}} {{member.last_name}}</h1>
                    <span class="member-header__ocupation">Figura Publica</span>
                    <span class='member-header__sentence' v-if="member.sentence">"{{member.sentence}}"</span>
                    <div>
                        <i class='fab fa-facebook'></i>
                        <i class='fab fa-instagram'></i>
                    </div>
                    <p>{{member.content}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    created: function () {
        this.getData();
    },
    data() {
        return {
            member: [],
        };
    },
    asyncData({ params, error }) {
        return axios
            .get(`/data/member/${params.id}.json`)
            .then((res) => {
                return { member_data: res.data };
            })
            .catch((e) => {
                error({ statusCode: 404, message: "Artist not found" });
            });
    },
    methods: {
        getData() {
            axios
                .get(`/data/member/${this.$route.params.id}.json`)
                .then((response) => {
                    this.member = response.data;
                });
        },
    },
    head() {
        return {
            title:
                this.member_data.name +
                " " +
                this.member_data.last_name +
                " - PUPILO X THES BEST CHAVA",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: this.member_data.content,
                },
                { property: "og:image", content: "https://pupiloxthesbestchava.netlify.app/cdn/img/team/" + this.member_data.id + ".jpg" },
                { name: "twitter:card", content: "summary" },
                // { name: "twitter:site", content: "@xpendmusic" },
                { name: "twitter:image", content: "https://pupiloxthesbestchava.netlify.app/cdn/img/team/" + this.member_data.id + ".jpg" },
            ],
        };
    },
};
</script>
<style lang="scss" scoped>
@import "~/assets/pages/team/id.scss";
</style>