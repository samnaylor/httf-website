<template>
  <div class="container text-2xl md:text-5xl lg:text-7xl">
    <span class="prompt">$</span>
    <span class="httf"></span>
    <span class="text"></span>
    <span class="cursor">_</span>
  </div>
</template>

<script>
import { gsap } from "gsap"
import { TextPlugin } from "gsap/TextPlugin"

gsap.registerPlugin(TextPlugin);

export default {
  name: 'Logo',
  data() {
    return {
      words: ['learn.it 🎓', 'code.it 👩‍💻', 'create.it 🚀']
    }
  },

  mounted() {
    let cursor = gsap.to('.cursor', {
      opacity: 0,
      ease: 'power2.inOut',
      duration: 0.75,
      repeat: -1
    })

    let masterTl = gsap.timeline().pause()

    let httf = gsap.timeline()
    httf.to('.httf', {
      duration: 2,
      text: 'httf://',
      onComplete: () => masterTl.play()
    });

    for (let i = 0; i < this.words.length; i++) {
      const word = this.words[i];
      const final = i === this.words.length - 1;

      let tl;
      if (final) {
        tl = gsap.timeline();
      } else {
        tl = gsap.timeline({
          repeat: 1,
          yoyo: true,
          repeatDelay: 1
        });
      }

      tl.to('.text', {
        duration: 1.5, text: word
      });
      masterTl.add(tl);
    }
  }
}
</script>

<style lang="postcss" scoped>

.container {
  @apply my-10 pl-2 flex text-center;
}

.prompt {
  @apply text-white mr-3;
}

</style>
