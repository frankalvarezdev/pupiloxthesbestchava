<template>
    <div>
        <div class='content'>
            <nav class='navbar'>
                <a href='/' class='navbar-brand'>PUPILO TV</a>
                <button class='navbar-toggler' @click='openNavbar'>
                    <i class='fa fa-bars'></i>
                </button>
                <div class='navbar-content' id='navbar-collapse'>
                    <div class='navbar-links' @click='openNavbar'>
                        <nuxt-link to='/'>Inicio</nuxt-link>

                        <nuxt-link to='/#team'>Equipo</nuxt-link>

                        <a
                            href='https://www.youtube.com/channel/UCoG6kpIgPKdsMfoDqrSmcEw/videos'
                            target='_blank'
                        >Videos</a>

                        <nuxt-link to='/blog'>Blog</nuxt-link>

                        <nuxt-link to='/acerca-de'>Acerca de</nuxt-link>

                        <nuxt-link to='/contacto'>Contacto</nuxt-link>
                    </div>
                    <div class='navbar-right' @click='openNavbar'>
                        <a
                            href='https://www.youtube.com/channel/UCoG6kpIgPKdsMfoDqrSmcEw'
                            target='_blank'
                        >
                            <i class='fab fa-youtube'></i>
                        </a>
                        <a href='https://www.instagram.com/pupiloxthesbestchava/' target='_blank'>
                            <i class='fab fa-instagram'></i>
                        </a>
                        <a
                            href='https://www.facebook.com/Pupilo-X-Thes-Best-Chava-104690264697369'
                            target='_blank'
                        >
                            <i class='fab fa-facebook'></i>
                        </a>
                        <a href>
                            <i class='fab fa-twitter'></i>
                        </a>
                    </div>
                </div>
            </nav>
            <Nuxt />
        </div>
        <footer class='footer'>
            <div>
                © 2021
                <strong>&nbsp;Pupilo X Thes Best Chava</strong>, Todos los derechos reservados.
            </div>
        </footer>
    </div>
</template>
<script>
export default {
    head() {
        return {
            script: [
                {
                    src: "https://kit.fontawesome.com/31ef3d53d0.js",
                },
            ],
            link: [
                {
                    rel: "stylesheet",
                    href:
                        "https://fonts.googleapis.com/css2?family=Hind:wght@300;400;500;600;700&family=Inter:wght@100;200;300;400;500;600;700&family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&display=swap",
                },
            ],
        };
    },
    methods: {
        openNavbar() {
            var nav = document.getElementById("navbar-collapse");
            nav.classList.toggle("navbar-show");
        },
    },
};
</script>
<style lang="scss">
@import "~/assets/config.scss";
@import "~ascendcss/ascendcss";

* {
    font-family: "Hind", sans-serif;
    font-family: "Inter", sans-serif;
    font-family: "Noto Sans", sans-serif;
}
a.nuxt-link-exact-active {
    color: lighten($bg, 50%) !important;
    font-weight: 600;
}

html {
    overflow-y: scroll;
}
/* width */
::-webkit-scrollbar {
    width: 8px;
}
/* Track */
::-webkit-scrollbar-track {
    background: $bg;
}

/* Handle */
::-webkit-scrollbar-thumb {
    background: lighten($bg, 15%);
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
    background: lighten($bg, 30%);
}

.navbar {
    a {
        text-decoration: none;
    }
    @include navbar($bg);
}
// @import url("mobstyle.css") screen and (max-width: 768px);
body {
    background: $bg;
    color: #fff;
    display: flex;
    flex-direction: column;
    position: relative;
    min-height: 100vh;
    padding-bottom: 60px;
}
.footer {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    height: 60px;
    background-color: $bg;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
}
</style>
