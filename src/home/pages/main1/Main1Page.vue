<template>
    <div>
        <div class="wrapper">
            <div class="content">
                <div class="panel">
                    <section class="textAnimation">
                        <h1 class="textT">T</h1>
                    </section>
                </div>

                <div class="panel panel2">
                    <section class="textAnimation2">
                        <h1 class="textEXT">ext</h1>
                    </section>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted, onUnmounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

let ctx;

onMounted(() => {
    ctx = gsap.context(() => {
        const panels = gsap.utils.toArray(".content .panel");

        gsap.to(".textT", {
            duration: 5,
            backgroundPosition: "100% 100%",
            ease: "power2.inOut",
        });

        gsap.to(".content", {
            x: () => -window.innerWidth * (panels.length - 1),
            ease: "none",
            scrollTrigger: {
                trigger: ".wrapper",
                start: "top top",
                end: "+=" + 100 * panels.length + "%",
                scrub: true,
                invalidateOnRefresh: true,
                pin: true,
            },
        });

        gsap.to(".textAnimation", {
            x: 1500,
            scrollTrigger: {
                trigger: ".textAnimation",
                start: "top top",
                end: "+=" + 100 * panels.length + "%",
                scrub: true,
                pin: true,
            },
        });

        gsap.to(".panel2", {
            x: 100,
            scrollTrigger: {
                trigger: ".panel2",
                start: "top top",
                end: "+=" + 100 * panels.length + "%",
                scrub: true,
                pin: true,
            },
        });
    });
});

onUnmounted(() => {
    ctx && ctx.revert();
});
</script>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: "Signika Negative", sans-serif, Arial;
    color: white;
}

.wrapper {
    width: 100%;
    height: 100vh;
    background-color: #202020;
    overflow: hidden;
}

.content {
    height: 100vh;
    display: flex;
    flex-wrap: nowrap;
}

.panel {
    flex: 1 0 100vw;
    color: var(--dark);
}

.textAnimation {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}

.textT {
    font-size: 80px;
    font-weight: bold;
    text-align: center;
    background: linear-gradient(0deg, #fff 50%, transparent 50%);
    -webkit-background-clip: text;
    -webkit-text-stroke: 1px #fff;
    background-clip: text;
    color: transparent;
    background-size: 100% 200%;
    background-position: 0% 0%;
}

.panel2 {
    background-color: #ffffff;
}

.textAnimation2 {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
}

.textEXT {
    font-size: 80px;
    font-weight: bold;
    text-align: center;
    color: #202020;
}

.center-svg {
    width: 100%;
    height: 100%;
    display: block;
}
</style>
