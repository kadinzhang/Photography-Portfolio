<template>
    <div>
        <!-- home START -->
        <div class="home-holder">
            <!-- home:logo START -->
            <div class="logo">
                <!-- <img
                    
                    src="https://coidea.website/demos/mh-portfolio-vuejs-and-gsap-template/static/logo.png"
                    alt="MH - Web Designer & Developer - Logo"
                >-->
                <p width="380" height="129" class="logo-txt">IAN
                    <br>DAILIS
                </p>
                <div class="logo-bg-holder">
                    <div class="logo-bg oval-big"></div>
                    <div class="logo-bg oval-small"></div>
                    <div class="logo-bg circle"></div>
                </div>
            </div>
            <!-- home:logo END -->
            <!-- home:custom-navigation START -->
            <div class="custom-navigation">
                <ul>
                    <li>
                        <router-link :to="'/photography'" exact>PHOTOGRAPHY</router-link>
                    </li>
                    <li>
                        <router-link :to="'/about'" exact>ABOUT</router-link>
                    </li>
                    <li>
                        <router-link :to="'/contact'" exact>CONTACT</router-link>
                    </li>
                </ul>
            </div>
            <!-- home:custom-navigation END -->
        </div>
        <!-- home END -->
    </div>
</template>

<script>
// gsap
import { TweenMax } from "gsap";
// scrollmagic
import ScrollMagic from "scrollmagic";
// jquery
import $ from "jquery";

export default {
    name: "Home",
    data() {
        return {};
    },
    mounted() {
        this.animateLogo();
    },
    methods: {
        animateLogo: function() {
            // comon -> sidebar -> navigation timeline
            let controller = new ScrollMagic.Controller(),
                timeline = new TimelineMax();

            timeline.set($(".logo .circle"), { scale: 0, z: 0.01 });
            timeline.set($(".logo .oval-small"), {
                autoAlpha: 0,
                scale: 0,
                z: 0.01
            });
            timeline.set($(".logo .oval-big"), {
                autoAlpha: 0,
                scale: 0,
                z: 0.01
            });
            timeline.set($(".logo .logo-txt"), { autoAlpha: 0, z: 0.01 });
            timeline.set($(".custom-navigation"), { autoAlpha: 0, z: 0.01 });

            timeline.fromTo(
                $(".logo .circle"),
                3,
                { scale: 0, transformOrigin: "50% 50%" },
                {
                    force3D: true,
                    scale: 1,
                    transformOrigin: "50% 50%",
                    ease: Back.easeOut.config(2.25)
                }
            );
            timeline.fromTo(
                $(".logo .oval-small"),
                2.5,
                { autoAlpha: 0, scale: 0, transformOrigin: "50% 50%" },
                {
                    force3D: true,
                    autoAlpha: 1,
                    scale: 1,
                    transformOrigin: "50% 50%",
                    ease: Back.easeOut.config(2.25)
                },
                "-=2.25"
            );
            timeline.fromTo(
                $(".logo .oval-big"),
                2.5,
                { autoAlpha: 0, scale: 0, transformOrigin: "50% 50%" },
                {
                    force3D: true,
                    autoAlpha: 1,
                    scale: 1,
                    transformOrigin: "50% 50%",
                    ease: Back.easeOut.config(2.25)
                },
                "-=2.25"
            );
            timeline.to(
                $(".logo .oval-big"),
                0,
                { className: "+=rotating-fast", ease: Expo.easeOut },
                "+=0.35"
            );
            timeline.to(
                $(".logo .oval-small"),
                0,
                { className: "+=rotating-slow", ease: Expo.easeOut },
                "+=0.35"
            );
            timeline.fromTo(
                $(".logo .logo-txt"),
                2.5,
                { autoAlpha: 0, x: -80 },
                { autoAlpha: 1, x: 0, ease: Expo.easeOut },
                "-=2.65"
            );
            timeline.fromTo(
                $(".custom-navigation"),
                2.5,
                { autoAlpha: 0, x: -80 },
                { autoAlpha: 1, x: 0, ease: Expo.easeOut },
                "-=2.45"
            );
        }
    }
};
</script>

<style lang="scss" scoped>
// mixins - media query
@mixin maxquery($width, $ratio: false) {
    @if $ratio {
        @media only screen and (max-width: $width) and (min--moz-device-pixel-ratio: $ratio),
            only screen and (max-width: $width) and (-webkit-min-device-pixel-ratio: $ratio),
            only screen and (max-width: $width) and (min-device-pixel-ratio: $ratio) {
            @content;
        }
    } @else {
        @media only screen and (max-width: $width) {
            @content;
        }
    }
}
.home-holder {
    position: absolute;
    display: block;
    width: 490px;
    height: auto;
    padding: 16px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    @include maxquery(640px) {
        width: 260px;
    }
    // logo
    .logo {
        position: relative;
        display: block;
        width: 100%;
        height: 100%;
        @include maxquery(640px) {
            width: 260px;
            height: auto;
        }
        .logo-txt {
            position: relative;
            z-index: 4;
            margin-left: -158px;
            margin-top: -40px;
            margin-bottom: 20px;
            font-size: 150px;
            font-weight: 100;
            font-family: "Raleway";
            font-weight: 600;
            line-height: 135px;
            color: white;
            @include maxquery(640px) {
                width: 280px;
                height: auto;
                margin: auto;
            }
            opacity: 0;
            visibility: hidden;
        }
        .logo-bg-holder {
            position: absolute;
            display: block;
            width: 620px;
            height: auto;
            margin-top: -107px;
            right: -68px;
            @include maxquery(640px) {
                width: 320px;
                height: auto;
                margin-top: -77px;
                right: -32px;
            }
        }
        .logo-bg {
            position: absolute;
            display: block;
            width: 100%;
            height: 100%;
            -moz-border-radius: 50%;
            -webkit-border-radius: 50%;
            border-radius: 50%;
            top: 50%;
            left: 50%;
            box-shadow: 0 0 36px rgba(0, 0, 0, 0.015),
                0 0 36px rgba(0, 0, 0, 0.05);
            &.oval-big {
                width: 540px;
                height: 580px;
                background: rgba(235, 235, 235, 0.1);
                margin-top: -290px;
                margin-left: -270px;
                z-index: 1;
                opacity: 0;
                visibility: hidden;
            }
            &.oval-small {
                width: 480px;
                height: 420px;
                background: rgba(235, 235, 235, 0.15);
                margin-top: -210px;
                margin-left: -240px;
                z-index: 2;
                opacity: 0;
                visibility: hidden;
            }
            &.circle {
                width: 360px;
                height: 360px;
                background: #a5d6a7;
                background: rgba(235, 235, 235, 0.25);
                transform: translate(-50%, -50%);
                z-index: 3;
            }
        }
    }
    // custom navigation
    .custom-navigation {
        position: relative;
        z-index: 5;
        opacity: 0;
        visibility: hidden;
        ul {
            position: relative;
            display: block;
            overflow: hidden;
            width: 100%;
            max-width: 450px;
            list-style-type: none;
            padding: 0;
            margin: 0;
            margin-left: -119px;
            @include maxquery(640px) {
                max-width: 100%;
                text-align: center;
                margin: 0;
            }
            li {
                position: relative;
                display: block;
                float: left;
                padding: 8px;
                @include maxquery(640px) {
                    display: inline;
                    float: none;
                    text-align: center;
                }
                a {
                    font-size: 23px;
                    font-weight: 500;
                    font-family: "Raleway";
                    text-decoration: none;
                    color: white !important;
                    opacity: 1;
                    transition: 0.5s !important;
                    &:hover {
                        opacity: 0.7;
                    }
                }
            }
        }
    }
}

@-webkit-keyframes rotating /* Safari and Chrome */ {
    from {
        -webkit-transform: rotate(0deg);
        -o-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    to {
        -webkit-transform: rotate(360deg);
        -o-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}
@keyframes rotating {
    from {
        -ms-transform: rotate(0deg);
        -moz-transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        -o-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    to {
        -ms-transform: rotate(360deg);
        -moz-transform: rotate(360deg);
        -webkit-transform: rotate(360deg);
        -o-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}
.rotating-fast {
    -webkit-animation: rotating 12s linear infinite;
    -moz-animation: rotating 12s linear infinite;
    -ms-animation: rotating 12s linear infinite;
    -o-animation: rotating 12s linear infinite;
    animation: rotating 12s linear infinite;
}
@-webkit-keyframes rotating-inverse /* Safari and Chrome */ {
    from {
        -webkit-transform: rotate(0deg);
        -o-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    to {
        -webkit-transform: rotate(-360deg);
        -o-transform: rotate(-360deg);
        transform: rotate(-360deg);
    }
}
@keyframes rotating-inverse {
    from {
        -ms-transform: rotate(0deg);
        -moz-transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        -o-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    to {
        -ms-transform: rotate(-360deg);
        -moz-transform: rotate(-360deg);
        -webkit-transform: rotate(-360deg);
        -o-transform: rotate(-360deg);
        transform: rotate(-360deg);
    }
}
.rotating-slow {
    -webkit-animation: rotating-inverse 16s linear infinite;
    -moz-animation: rotating-inverse 16s linear infinite;
    -ms-animation: rotating-inverse 16s linear infinite;
    -o-animation: rotating-inverse 16s linear infinite;
    animation: rotating-inverse 16s linear infinite;
}
@media only screen and (max-width: 1400px) {
    .logo-bg {
        position: absolute;
        display: block;
        width: 100%;
        height: 100%;
        -moz-border-radius: 50%;
        -webkit-border-radius: 50%;
        border-radius: 50%;
        top: 50%;
        left: 50%;
        box-shadow: 0 0 36px rgba(0, 0, 0, 0.015), 0 0 36px rgba(0, 0, 0, 0.05);
        &.oval-big {
            width: 440px;
            height: 480px;
            background: rgba(235, 235, 235, 0.1);
            margin-top: -290px;
            margin-left: -270px;
            z-index: 1;
            opacity: 0;
            visibility: hidden;
        }
        &.oval-small {
            width: 380px;
            height: 320px;
            background: rgba(235, 235, 235, 0.15);
            margin-top: -210px;
            margin-left: -240px;
            z-index: 2;
            opacity: 0;
            visibility: hidden;
        }
        &.circle {
            width: 260px;
            height: 260px;
            background: #a5d6a7;
            background: rgba(235, 235, 235, 0.25);
            transform: translate(-50%, -50%);
            z-index: 3;
        }
    }
}
</style>