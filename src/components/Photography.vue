<template>
    <section>
        <h1>I shoot</h1>
        <div class="swiper-container slideshow">
            <div class="swiper-wrapper">
                <div class="swiper-slide slide">
                    <div
                        class="slide-image"
                        style="background-image: url(https://lh3.googleusercontent.com/-n-6bV10-NlU/XFeNw0yh0dI/AAAAAAAAHcs/_dLyfP9WVRUgxJnyetLVPuVxKstZcr9DwCL0BGAYYCw/h1367/LSD_6288.jpg)"
                    ></div>
                    <span class="slide-title">Landscapes</span>
                </div>

                <div class="swiper-slide slide">
                    <div
                        class="slide-image"
                        style="background-image: url(https://lh3.googleusercontent.com/-Miutl7MiUi4/XE3b02-e-aI/AAAAAAAAHSM/0CkrK5qqI9AtVEmvDJXj_JogoHqzHiPnwCL0BGAYYCw/h1170/Madrid%2BPanorama%2Bflat.jpg"
                    ></div>
                    <span class="slide-title">Cities</span>
                </div>

                <div class="swiper-slide slide">
                    <div
                        class="slide-image"
                        style="background-image: url(https://lh3.googleusercontent.com/-l9SCTL58XB4/XE4DO-tlVrI/AAAAAAAAHWM/QrFZjtUALZI9KKe0E8GEVmAqmW9b_GF0QCL0BGAYYCw/h1367/LSD_5129.jpg"
                    ></div>
                    <span class="slide-title">Macros</span>
                </div>
                <div class="swiper-slide slide">
                    <div
                        class="slide-image"
                        style="background-image: url(https://lh3.googleusercontent.com/-hYFOY2FZ1JM/XE4C_WH4BqI/AAAAAAAAHWE/NHS9fqEF9Nc6lMMRc2TPaqF1hkBDeu2hgCL0BGAYYCw/h1367/LSD_4973.jpg"
                    ></div>
                    <span class="slide-title">Animals</span>
                </div>
            </div>
            <div class="buttonholder">
                <button class="button">
                    <router-link class="link" :to="'/gallery'" exact>SEE MORE</router-link>

                    <div class="button__horizontal"></div>
                    <div class="button__vertical"></div>
                </button>
            </div>
            <div class="slideshow-pagination"></div>

            <div class="slideshow-navigation">
                <div class="slideshow-navigation-button prev">
                    <span class="fas fa-chevron-left"></span>
                </div>
                <div class="slideshow-navigation-button next">
                    <span class="fas fa-chevron-right"></span>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "Photography",
    mounted: () => {
        // The Slideshow class.
        class Slideshow {
            constructor(el) {
                this.DOM = { el: el };

                this.config = {
                    slideshow: {
                        delay: 5000,
                        pagination: {
                            duration: 5
                        }
                    }
                };

                // Set the slideshow
                this.init();
            }
            init() {
                var self = this;

                // Charmed title
                this.DOM.slideTitle = this.DOM.el.querySelectorAll(
                    ".slide-title"
                );
                this.DOM.slideTitle.forEach(slideTitle => {
                    charming(slideTitle);
                });

                // Set the slider
                this.slideshow = new Swiper(this.DOM.el, {
                    loop: true,
                    autoplay: {
                        delay: this.config.slideshow.delay,
                        disableOnInteraction: false
                    },
                    speed: 500,
                    preloadImages: true,
                    updateOnImagesReady: true,

                    pagination: {
                        el: ".slideshow-pagination",
                        clickable: true,
                        bulletClass: "slideshow-pagination-item",
                        bulletActiveClass: "active",
                        clickableClass: "slideshow-pagination-clickable",
                        modifierClass: "slideshow-pagination-",
                        renderBullet: function(index, className) {
                            var slideIndex = index,
                                number =
                                    index <= 8
                                        ? "0" + (slideIndex + 1)
                                        : slideIndex + 1;

                            var paginationItem =
                                '<span class="slideshow-pagination-item">';
                            paginationItem +=
                                '<span class="pagination-number">' +
                                number +
                                "</span>";
                            paginationItem =
                                index <= 8
                                    ? paginationItem +
                                      '<span class="pagination-separator"><span class="pagination-separator-loader"></span></span>'
                                    : paginationItem;
                            paginationItem += "</span>";

                            return paginationItem;
                        }
                    },

                    // Navigation arrows
                    navigation: {
                        nextEl: ".slideshow-navigation-button.next",
                        prevEl: ".slideshow-navigation-button.prev"
                    },

                    // And if we need scrollbar
                    scrollbar: {
                        el: ".swiper-scrollbar"
                    },

                    on: {
                        init: function() {
                            self.animate("next");
                        }
                    }
                });

                // Init/Bind events.
                this.initEvents();
            }
            initEvents() {
                this.slideshow.on("paginationUpdate", (swiper, paginationEl) =>
                    this.animatePagination(swiper, paginationEl)
                );
                //this.slideshow.on('paginationRender', (swiper, paginationEl) => this.animatePagination());

                this.slideshow.on("slideNextTransitionStart", () =>
                    this.animate("next")
                );

                this.slideshow.on("slidePrevTransitionStart", () =>
                    this.animate("prev")
                );
            }
            animate(direction = "next") {
                // Get the active slide
                (this.DOM.activeSlide = this.DOM.el.querySelector(
                    ".swiper-slide-active"
                )),
                    (this.DOM.activeSlideImg = this.DOM.activeSlide.querySelector(
                        ".slide-image"
                    )),
                    (this.DOM.activeSlideTitle = this.DOM.activeSlide.querySelector(
                        ".slide-title"
                    )),
                    (this.DOM.activeSlideTitleLetters = this.DOM.activeSlideTitle.querySelectorAll(
                        "span"
                    ));

                // Reverse if prev
                this.DOM.activeSlideTitleLetters =
                    direction === "next"
                        ? this.DOM.activeSlideTitleLetters
                        : [].slice
                              .call(this.DOM.activeSlideTitleLetters)
                              .reverse();

                // Get old slide
                this.DOM.oldSlide =
                    direction === "next"
                        ? this.DOM.el.querySelector(".swiper-slide-prev")
                        : this.DOM.el.querySelector(".swiper-slide-next");
                if (this.DOM.oldSlide) {
                    // Get parts
                    (this.DOM.oldSlideTitle = this.DOM.oldSlide.querySelector(
                        ".slide-title"
                    )),
                        (this.DOM.oldSlideTitleLetters = this.DOM.oldSlideTitle.querySelectorAll(
                            "span"
                        ));
                    // Animate
                    this.DOM.oldSlideTitleLetters.forEach((letter, pos) => {
                        TweenMax.to(letter, 0.3, {
                            ease: Quart.easeIn,
                            delay:
                                (this.DOM.oldSlideTitleLetters.length -
                                    pos -
                                    1) *
                                0.04,
                            y: "50%",
                            opacity: 0
                        });
                    });
                }

                // Animate title
                this.DOM.activeSlideTitleLetters.forEach((letter, pos) => {
                    TweenMax.to(letter, 0.6, {
                        ease: Back.easeOut,
                        delay: pos * 0.05,
                        startAt: { y: "50%", opacity: 0 },
                        y: "0%",
                        opacity: 1
                    });
                });

                // Animate background
                TweenMax.to(this.DOM.activeSlideImg, 1.5, {
                    ease: Expo.easeOut,
                    startAt: { x: direction === "next" ? 200 : -200 },
                    x: 0
                });

                //this.animatePagination()
            }
            animatePagination(swiper, paginationEl) {
                // Animate pagination
                this.DOM.paginationItemsLoader = paginationEl.querySelectorAll(
                    ".pagination-separator-loader"
                );
                this.DOM.activePaginationItem = paginationEl.querySelector(
                    ".slideshow-pagination-item.active"
                );
                this.DOM.activePaginationItemLoader = this.DOM.activePaginationItem.querySelector(
                    ".pagination-separator-loader"
                );

                console.log(swiper.pagination);
                // console.log(swiper.activeIndex);

                // Reset and animate
                TweenMax.set(this.DOM.paginationItemsLoader, { scaleX: 0 });
                TweenMax.to(
                    this.DOM.activePaginationItemLoader,
                    this.config.slideshow.pagination.duration,
                    {
                        startAt: { scaleX: 0 },
                        scaleX: 1
                    }
                );
            }
        }

        const slideshow = new Slideshow(document.querySelector(".slideshow"));
    }
};
</script>

<style lang="scss">
html,
body {
    overflow-y: visible !important;
}
.buttonholder {
    position: absolute;
    width: 100%;
    text-align: center;
    top: 55vh;
    margin: auto;
    z-index: 2;
}
.button {
    --offset: 10px;
    --border-size: 2px;

    display: block;
    font-family: "Raleway", sans-serif !important;
    position: relative;
    padding: 0;
    appearance: none;
    padding: 1.5em 0em;

    border: 0;
    background: transparent;
    color: white;
    text-transform: uppercase;
    letter-spacing: 0.25em;
    outline: none;
    cursor: pointer;
    font-weight: bold;
    font-size: 17px;
    border-radius: 0;
    box-shadow: inset 0 0 0 var(--border-size) currentcolor;
    transition: background 0.8s ease;
    margin: auto;
    a {
        padding: 1.5em 3em;
        width: 200px;
        height: 100px;
        color: white !important;
    }
    &:hover {
        background: rgba(100, 0, 0, 0.03);
    }

    &__horizontal,
    &__vertical {
        position: absolute;
        top: var(--horizontal-offset, 0);
        right: var(--vertical-offset, 0);
        bottom: var(--horizontal-offset, 0);
        left: var(--vertical-offset, 0);
        transition: transform 0.3s ease;
        will-change: transform;

        &::before {
            content: "";
            position: absolute;
            border: inherit;
        }
    }

    &__horizontal {
        --vertical-offset: calc(var(--offset) * -1);
        border-top: var(--border-size) solid currentcolor;
        border-bottom: var(--border-size) solid currentcolor;

        &::before {
            top: calc(var(--vertical-offset) - var(--border-size));
            bottom: calc(var(--vertical-offset) - var(--border-size));
            left: calc(var(--vertical-offset) * -1);
            right: calc(var(--vertical-offset) * -1);
        }
    }

    &:hover &__horizontal {
        transform: scaleX(0);
    }

    &__vertical {
        --horizontal-offset: calc(var(--offset) * -1);
        border-left: var(--border-size) solid currentcolor;
        border-right: var(--border-size) solid currentcolor;

        &::before {
            top: calc(var(--horizontal-offset) * -1);
            bottom: calc(var(--horizontal-offset) * -1);
            left: calc(var(--horizontal-offset) - var(--border-size));
            right: calc(var(--horizontal-offset) - var(--border-size));
        }
    }

    &:hover &__vertical {
        transform: scaleY(0);
    }
}
section {
    position: relative;
    width: 100vw !important;
    left: 0;
    height: calc(-100px + 100vh) !important;
    h1 {
        position: absolute;
        width: 100%;
        top: 32vh;
        font-size: 3rem !important;
        margin: auto;
        color: white;
        font-family: "Oswald", sans-serif !important;
        text-align: center;
        z-index: 69;
    }
}

.swiper-container {
    width: 100%;
    height: 100%;
}

.slide {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    text-align: center;
    font-size: 18px;
    background: #fff;
    overflow: hidden;
    &-image {
        position: absolute;
        top: -200px;
        left: -200px;
        width: calc(100% + 400px);
        height: calc(100% + 400px);
        background-position: 50% 50%;
        background-size: cover;
    }
    &-title {
        margin-top: -2rem;
        font-size: 4rem;
        line-height: 1;
        max-width: 50%;
        white-space: normal;
        word-break: break-word;
        color: #fff;
        z-index: 100;
        font-family: "Oswald", sans-serif;
        text-transform: uppercase;
        font-weight: 400;
        @media (min-width: 45em) {
            font-size: 7vw;
            max-width: none;
        }
        span {
            white-space: pre;
            display: inline-block;
            opacity: 0;
        }
    }
}

.slideshow {
    position: relative;

    &-pagination {
        position: absolute;
        bottom: 5rem;
        left: 0;
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        transition: 0.3s opacity;
        z-index: 10;
        &-item {
            display: flex;
            align-items: center;
            .pagination-number {
                opacity: 0.6;
            }
            &:hover,
            &:focus {
                cursor: pointer;
            }
            &:last-of-type {
                .pagination-separator {
                    width: 0;
                }
            }
            &.active {
                .pagination-number {
                    opacity: 1;
                }
                .pagination-separator {
                    width: 10vw;
                }
                //.pagination-separator-loader {
                //  transform: scaleX(1);
                //  transition: all 3s ease;
                //}
            }
        }
    }

    &-navigation {
        &-button {
            position: absolute;
            top: 0rem;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100%;
            width: 5rem;
            z-index: 1000;
            transition: all 0.3s ease;
            color: #fff;
            &:hover,
            &:focus {
                cursor: pointer;
                background: rgba(#000, 0.5);
            }
            &.prev {
                left: 0;
            }
            &.next {
                right: 0;
            }
        }
    }
}

.pagination-number {
    font-size: 2.2rem;
    color: #fff;
    font-family: "Oswald", sans-serif;
    padding: 0 0.5rem;
}

.pagination-separator {
    display: none;
    @media (min-width: 45em) {
        display: block;
    }
    position: relative;
    width: 40px;
    height: 2px;
    background: rgba(#ffffff, 0.35);
    transition: all 0.3s ease;
    &-loader {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #ffffff;
        transform-origin: 0 0;
    }
}
@media only screen and (max-width: 1500px) {
    section {
        height: calc(-86px + 100vh) !important;
        .slideshow-pagination {
            bottom: 2rem;
        }
        h1 {
            top: 23vh;
            font-size: 2rem !important;
        }
        .slide-title {
            margin-top: -4rem;
        }
        .buttonholder {
            top: 52vh;
            .button {
                padding: 1rem 0rem;
                a {
                    padding: 2rem 2rem;
                }
            }
        }
    }
}
@media only screen and (max-width: 600px) {
    section h1 {
        font-size: 25px !important;
        margin-top: 80px;
    }
    .slide-title {
        font-size: 40px;
        margin-top: -0rem !important;
    }
    .button {
        padding: 1rem;
    }
    .button a {
        padding: 0rem 1rem;
    }
}
</style>
