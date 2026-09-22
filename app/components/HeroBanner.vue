<!-- components/HeroBanner.vue -->
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import emblaCarouselVue from 'embla-carousel-vue'
import Autoplay from 'embla-carousel-autoplay'
import gsap from 'gsap'

// Initialize Embla Carousel with Autoplay Plugin
const [emblaRef, emblaApi] = emblaCarouselVue({ loop: true }, [
  Autoplay({ delay: 4500, stopOnInteraction: false, stopOnMouseEnter: true })
])

const activeIndex = ref(0)

const slides = [
  {
    title: 'সুই-সুতায় বোনা <br /><span class="text-amber-400">বাংলার ঐতিহ্য ও সংস্কৃতি</span>',
    desc: 'পল্লীকবি জসীম উদ্‌দীনের উপাখ্যানের অনুপ্রেরণায় গ্রামীণ কারিগরদের নিজ হাতে সেলাই করা অরিজিনাল জামালপুরি নকশী কাঁথা।',
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=1200',
    tag: '✨ জিআই স্বীকৃতিপ্রাপ্ত হস্তশিল্প'
  },
  {
    title: 'বেডরুমের আভিজাত্যে <br /><span class="text-amber-400">হাতে সেলাইয়ের নকশী বেডশীট</span>',
    desc: 'প্রাকৃতিক সুতি কাপড়ে ১০০% পাকা রঙের সুই-সুতোর কারুকাজ। ঘরকে দিন এক টুকরো ঐতিহ্যময় আভিজাত্য।',
    image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=1200',
    tag: '🌿 ১০০% খাঁটি কটন ফেব্রিক'
  },
  {
    title: 'কোমল তুলতুলে <br /><span class="text-amber-400">বেবি নকশী কাঁথা কম্বো</span>',
    desc: 'নবজাতক সোনামণিদের ত্বকের সুরক্ষায় শতভাগ সুতি কাপড়ে তৈরি আরামদায়ক ও নিরাপদ কাঁথা সেট।',
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=1200',
    tag: '👶 শিশুদের জন্য স্পেশাল'
  }
]

// Smooth GSAP slide transition animation
const animateSlide = (index: number) => {
  const slideEl = document.querySelector(`.slide-content-${index}`)
  if (!slideEl) return

  const badge = slideEl.querySelector('.gsap-badge')
  const title = slideEl.querySelector('.gsap-title')
  const desc = slideEl.querySelector('.gsap-desc')
  const btns = slideEl.querySelectorAll('.gsap-btn')

  const tl = gsap.timeline()
  tl.fromTo(badge, { y: -15, opacity: 0 }, { y: 0, opacity: 1, duration: 0.5, ease: 'power2.out' })
    .fromTo(title, { y: 25, opacity: 0 }, { y: 0, opacity: 1, duration: 0.7, ease: 'power3.out' }, '-=0.3')
    .fromTo(desc, { y: 15, opacity: 0 }, { y: 0, opacity: 1, duration: 0.5, ease: 'power2.out' }, '-=0.4')
    .fromTo(btns, { scale: 0.9, opacity: 0 }, { scale: 1, opacity: 1, duration: 0.4, stagger: 0.1, ease: 'back.out(1.5)' }, '-=0.2')
}

onMounted(() => {
  if (!emblaApi.value) return

  const onSelect = () => {
    if (!emblaApi.value) return
    activeIndex.value = emblaApi.value.selectedScrollSnap()
    animateSlide(activeIndex.value)
  }

  emblaApi.value.on('select', onSelect)
  // Run initial animation
  setTimeout(() => animateSlide(0), 100)
})

const scrollPrev = () => emblaApi.value?.scrollPrev()
const scrollNext = () => emblaApi.value?.scrollNext()
</script>

<template>
  <section class="w-full max-w-7xl mx-auto px-4 py-6">
    <div class="relative rounded-3xl overflow-hidden shadow-2xl bg-slate-950 text-white">
      <!-- Carousel Viewport -->
      <div ref="emblaRef" class="overflow-hidden">
        <div class="flex">
          <div
            v-for="(slide, index) in slides"
            :key="index"
            class="flex-[0_0_100%] min-w-0 relative min-h-[500px] lg:min-h-[580px] flex items-center p-8 sm:p-16"
          >
            <!-- Background Image -->
            <img
              :src="slide.image"
              class="absolute inset-0 w-full h-full object-cover opacity-35"
              alt="Nakshi Banner"
            />
            <div class="absolute inset-0 bg-gradient-to-r from-slate-950/90 via-slate-950/60 to-transparent"></div>

            <!-- Content -->
            <div :class="`slide-content-${index}`" class="relative z-10 max-w-2xl space-y-6">
              <span class="gsap-badge inline-block border border-amber-400 text-amber-300 bg-amber-950/50 backdrop-blur px-4 py-1.5 rounded-full text-xs sm:text-sm font-semibold">
                {{ slide.tag }}
              </span>

              <h1
                class="gsap-title text-3xl sm:text-5xl lg:text-6xl font-extrabold font-serif leading-tight text-white"
                v-html="slide.title"
              ></h1>

              <p class="gsap-desc text-slate-200 text-sm sm:text-base leading-relaxed">
                {{ slide.desc }}
              </p>

              <div class="flex flex-wrap gap-4 pt-2">
                <button class="gsap-btn bg-amber-500 hover:bg-amber-600 text-slate-950 font-bold px-8 py-3.5 rounded-xl shadow-lg transition-all active:scale-95">
                  সব কালেকশন দেখুন →
                </button>
                <button class="gsap-btn border border-white/30 text-white hover:bg-white/10 px-8 py-3.5 rounded-xl backdrop-blur transition-all active:scale-95">
                  অফারগুলো দেখুন
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Navigation Arrows -->
      <button
        @click="scrollPrev"
        class="absolute left-4 top-1/2 -translate-y-1/2 w-11 h-11 rounded-full bg-white/20 hover:bg-white/40 text-white flex items-center justify-center backdrop-blur transition-all z-20"
      >
        ❮
      </button>
      <button
        @click="scrollNext"
        class="absolute right-4 top-1/2 -translate-y-1/2 w-11 h-11 rounded-full bg-white/20 hover:bg-white/40 text-white flex items-center justify-center backdrop-blur transition-all z-20"
      >
        ❯
      </button>
    </div>
  </section>
</template>