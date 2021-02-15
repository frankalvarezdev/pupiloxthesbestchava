<template>
    <div>
        <div class='member-header'>
            <div class='member-header__left'>
                <svg
                    xmlns='http://www.w3.org/2000/svg'
                    viewBox='0 0 24 24'
                    :style='`background-image: url(${member.img})`'
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
                    <h1 class='member-header__title'>{{member.name}}</h1>
                    <span class='member-header__ocupation'>{{member.occupation}}</span>
                    <span
                        class='member-header__sentence'
                        v-if='member.sentence'
                    >"{{member.sentence}}"</span>
                    <div v-if="member.social_media">
                        <span v-for='social of member.social_media' :key='social'>
                            <a :href="social.url" target="_blank" style="color: #fff">
                                <i :class='`fa fa-${social.name}`'></i>
                            </a>&nbsp;
                        </span>
                    </div>
                    <nuxt-content class='aricle-content' :document='member' />
                </div>
            </div>
        </div>
    </div>
</template>
 
<script>
import axios from "axios";

export default {
    async asyncData({ $content, params }) {
        const member = await $content("team", params.id).fetch();

        return { member };
    },
    head() {
        return {
            title: this.member.name + " - PUPILO X THES BEST CHAVA",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: this.member.description,
                },
                {
                    property: "og:image",
                    content:
                        "https://pupiloxthesbestchava.netlify.app" +
                        this.member.img,
                },
                { name: "twitter:card", content: "summary" },
                // { name: "twitter:site", content: "@xpendmusic" },
                {
                    name: "twitter:image",
                    content:
                        "https://pupiloxthesbestchava.netlify.app" +
                        this.member.img,
                },
            ],
        };
    },
};
</script>
<style lang="scss" scoped>
@import "~/assets/pages/team/id.scss";
</style>