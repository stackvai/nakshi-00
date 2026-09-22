<!-- pages/index.vue -->
<script setup lang="ts">
import { ref } from 'vue'

const selectedProduct = ref<any>(null)
const activeFaq = ref<number | null>(null)

// Trending & Top-Selling Product Collections
const trendingProducts = [
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, originalPrice: 5200, category: 'double', tag: 'হট সেলিং', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 2, title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট', price: 3200, originalPrice: 3700, category: 'bedsheet', tag: 'পাকা রং', image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
  { id: 3, title: 'হাতে সেলাই করা সুতি নকশী তিন-পিস', price: 2450, originalPrice: 2900, category: 'attire', tag: 'নতুন ডিজাইন', image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=600' },
  { id: 4, title: 'ভিক্টোরিয়ান লাল-হলুদ সিঙ্গেল কদম কাঁথা', price: 2750, originalPrice: 3100, category: 'single', tag: 'জনপ্রিয়', image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' }
]

const giCertifiedProducts = [
  { id: 5, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, originalPrice: 4200, category: 'double', tag: 'জিআই সার্টিফাইড', image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 6, title: 'মাদারগঞ্জ স্পেশাল ফ্লাওয়ার নকশী কাঁথা', price: 4100, originalPrice: 4600, category: 'double', tag: 'জিআই সার্টিফাইড', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 7, title: 'মেলান্দহ ক্লাসিক মাস্টারপিস কাঁথা', price: 4900, originalPrice: 5500, category: 'double', tag: 'জিআই সার্টিফাইড', image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
  { id: 8, title: 'ঐতিহ্যবাহী লতা-পাতা নকশী বেডশীট', price: 3500, originalPrice: 4000, category: 'bedsheet', tag: 'জিআই সার্টিফাইড', image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=600' }
]

const babyEssentialsProducts = [
  { id: 9, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', price: 1850, originalPrice: 2200, category: 'baby', tag: 'সফট কটন', image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' },
  { id: 10, title: 'নবজাতকের রঙিন সুতি কুশন ও কাঁথা সেট', price: 1450, originalPrice: 1750, category: 'baby', tag: 'বেবি স্পেশাল', image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 11, title: 'হাতে বোনা মিনি বেবি নকশী কাঁথা', price: 950, originalPrice: 1200, category: 'baby', tag: 'সেরা দাম', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 12, title: 'সফট কটন বেবি র‍্যাপার কাঁথা', price: 1250, originalPrice: 1500, category: 'baby', tag: 'আরামদায়ক', image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' }
]

const faqs = [
  { q: 'আপনাদের নকশী কাঁথাগুলো কি সম্পূর্ণ হাতে সেলাই করা?', a: 'হ্যাঁ! আমাদের প্রতিটি পণ্য জামালপুরের অভিজ্ঞ নারী কারিগরদের দ্বারা শতভাগ নিজ হাতে সেলাই করা।' },
  { q: 'ধোয়ার পর কাপড়ের রং কি উঠে যাবে?', a: 'একদমই না। আমরা ১০০% পাকা রঙের প্রি-ওয়াশড কটন সুতা ও সুতি কাপড় ব্যবহার করি।' },
  { q: 'ডেলিভারির সময় কি প্রোডাক্ট দেখে পেমেন্ট করা যাবে?', a: 'অবশ্যই! আমাদের ক্যাশ অন ডেলিভারি সুবিধায় প্রোডাক্ট চেক করে পেমেন্ট করতে পারবেন।' }
]
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-20 lg:space-y-28 pb-16">

    <!-- 1. Hero Banner Component -->
    <HeroBanner />

    <!-- 2. Value Propositions Bar -->
    <section class="grid grid-cols-2 md:grid-cols-4 gap-4">
      <div v-for="(v, i) in [
        { icon: '🧵', title: '১০০% হস্তশিল্প', desc: 'মেশিনের ছোঁয়া ছাড়া হাতে সেলাই' },
        { icon: '📦', title: 'দেখে পেমেন্ট', desc: 'ডেলিভারির সময় চেক করার সুবিধা' },
        { icon: '🌿', title: 'পাকা রং নিশ্চিত', desc: '১০০% প্রিমিয়াম সুতি কাপড়' },
        { icon: '🤝', title: 'কাস্টম অর্ডার', desc: 'পছন্দমতো সাইজ ও ডিজাইনে তৈরি' }
      ]" :key="i" class="p-5 bg-white rounded-2xl border border-slate-100 shadow-sm flex items-center gap-4">
        <div class="w-12 h-12 rounded-xl bg-amber-50 text-xl flex items-center justify-center shrink-0">{{ v.icon }}</div>
        <div>
          <h3 class="font-bold text-slate-900 text-sm font-serif">{{ v.title }}</h3>
          <p class="text-xs text-slate-500 mt-0.5">{{ v.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 3. Featured Categories Grid -->
    <section class="space-y-6">
      <div class="flex justify-between items-end border-b border-slate-100 pb-4">
        <div>
          <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">ক্যাটাগরি</span>
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 mt-1">পছন্দের ক্যাটাগরি বেছে নিন</h2>
        </div>
      </div>
      <div class="grid grid-cols-2 lg:grid-cols-4 gap-6">
        <div v-for="(cat, i) in [
          { title: 'ডাবল নকশী কাঁথা', count: '১২০+ পণ্য', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
          { title: 'সিঙ্গেল ও বেবি কাঁথা', count: '৮৫+ পণ্য', image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' },
          { title: 'নকশী বেডশীট', count: '৬৪+ পণ্য', image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
          { title: 'হাতের কাজের থ্রি-পিস', count: '১৫০+ পণ্য', image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=600' },
        ]" :key="i" class="group relative overflow-hidden rounded-2xl aspect-[3/4] cursor-pointer">
          <img :src="cat.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt="Category" />
          <div class="absolute inset-0 bg-gradient-to-t from-slate-950/90 via-slate-950/20 to-transparent"></div>
          <div class="absolute bottom-0 p-5 text-white">
            <span class="inline-block bg-amber-500 text-slate-950 text-xs font-bold px-2.5 py-1 rounded-md mb-2">{{ cat.count }}</span>
            <h3 class="text-lg font-bold font-serif group-hover:text-amber-300 transition-colors">{{ cat.title }}</h3>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. Heritage & Artisan Storytelling -->
    <section class="bg-rose-950 text-white rounded-3xl p-8 sm:p-14 relative overflow-hidden">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <div class="space-y-6">
          <span class="inline-block bg-amber-500/20 text-amber-300 border border-amber-400/30 text-xs px-3 py-1 rounded-full">ঐতিহ্যের গল্প</span>
          <h2 class="text-3xl sm:text-4xl font-extrabold font-serif leading-snug">
            "এমনি করিয়া পার হয়ে গেল কত যে দীর্ঘ দিন... <br />
            নকশী কাঁথার মাঠের কাহিনী হইলো না শেষ কভু"
          </h2>
          <p class="text-rose-100/90 text-sm leading-relaxed">
            জামালপুরের মহিলারা শত শত বছর ধরে নিজেদের আবেগ ও ভালোবাসা সেলাইয়ের ফোঁড়ে ফোঁড়ে তুলে এনেছেন। আমাদের প্রতিটি কাঁথা জামালপুরি জিআই সনদপ্রাপ্ত অরিজিনাল হস্তশিল্প।
          </p>
        </div>
        <div class="rounded-2xl overflow-hidden aspect-[4/3] border-4 border-white/10">
          <img src="https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=800" class="w-full h-full object-cover" alt="Artisan Story" />
        </div>
      </div>
    </section>

    <!-- 5. Section A: 🔥 টপ ট্রেন্ডিং কালেকশন (4 Items Grid) -->
    <section class="space-y-8">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 border-b border-slate-100 pb-4">
        <div>
          <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">সেরা চাহিদা</span>
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 mt-1">🔥 টপ ট্রেন্ডিং কালেকশন</h2>
        </div>
        <button class="text-xs font-bold text-rose-900 hover:text-rose-950 underline">সব দেখুন →</button>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div v-for="product in trendingProducts" :key="product.id" class="bg-white rounded-2xl border border-slate-100 overflow-hidden shadow-sm hover:shadow-md transition-shadow flex flex-col justify-between">
          <div>
            <div class="relative aspect-[4/3] overflow-hidden bg-slate-100">
              <span v-if="product.tag" class="absolute top-3 left-3 z-10 bg-rose-900 text-white text-xs font-bold px-2.5 py-1 rounded">{{ product.tag }}</span>
              <img :src="product.image" class="w-full h-full object-cover" :alt="product.title" />
            </div>
            <div class="p-4 space-y-2">
              <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1">{{ product.title }}</h3>
            </div>
          </div>
          <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <div>
              <span class="text-base font-extrabold text-rose-950">৳ {{ product.price }}</span>
              <span class="text-xs text-slate-400 line-through ml-1.5">৳ {{ product.originalPrice }}</span>
            </div>
            <button @click="selectedProduct = product" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3 py-1.5 rounded-lg transition-colors">
              দ্রুত দেখুন
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- 6. GI Certification Banner -->
    <section class="bg-amber-50 rounded-3xl p-8 border border-amber-200 flex flex-col md:flex-row items-center justify-between gap-6">
      <div class="flex items-center gap-6">
        <div class="w-16 h-16 rounded-2xl bg-amber-500 text-slate-950 font-bold flex items-center justify-center text-xl shrink-0 font-serif">
          জিআই
        </div>
        <div>
          <h3 class="text-xl font-bold text-slate-900 font-serif">জামালপুরের ভৌগোলিক নির্দেশক (GI) সনদপ্রাপ্ত পণ্য</h3>
          <p class="text-sm text-slate-600 mt-1">আমাদের প্রতিটি কাঁথায় অরিজিনাল জামালপুরি হস্তশিল্পের গুণগত মান নিশ্চিত করা হয়।</p>
        </div>
      </div>
    </section>

    <!-- 7. Section B: ✨ জিআই সার্টিফাইড মাস্টারপিস (4 Items Grid) -->
    <section class="space-y-8">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 border-b border-slate-100 pb-4">
        <div>
          <span class="text-xs font-bold text-amber-800 uppercase tracking-wider">অরিজিনাল ঐতিহ্য</span>
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 mt-1">✨ জিআই সার্টিফাইড মাস্টারপিস</h2>
        </div>
        <button class="text-xs font-bold text-rose-900 hover:text-rose-950 underline">সব দেখুন →</button>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div v-for="product in giCertifiedProducts" :key="product.id" class="bg-white rounded-2xl border border-slate-100 overflow-hidden shadow-sm hover:shadow-md transition-shadow flex flex-col justify-between">
          <div>
            <div class="relative aspect-[4/3] overflow-hidden bg-slate-100">
              <span v-if="product.tag" class="absolute top-3 left-3 z-10 bg-amber-600 text-white text-xs font-bold px-2.5 py-1 rounded">{{ product.tag }}</span>
              <img :src="product.image" class="w-full h-full object-cover" :alt="product.title" />
            </div>
            <div class="p-4 space-y-2">
              <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1">{{ product.title }}</h3>
            </div>
          </div>
          <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <div>
              <span class="text-base font-extrabold text-rose-950">৳ {{ product.price }}</span>
              <span class="text-xs text-slate-400 line-through ml-1.5">৳ {{ product.originalPrice }}</span>
            </div>
            <button @click="selectedProduct = product" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3 py-1.5 rounded-lg transition-colors">
              দ্রুত দেখুন
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- 8. Section C: 🍼 সফট বেবি কাঁথা কম্বো (4 Items Grid) -->
    <section class="space-y-8">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 border-b border-slate-100 pb-4">
        <div>
          <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">ছোটদের জন্য</span>
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 mt-1">🍼 কোমল বেবি কাঁথা ও কম্বো</h2>
        </div>
        <button class="text-xs font-bold text-rose-900 hover:text-rose-950 underline">সব দেখুন →</button>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div v-for="product in babyEssentialsProducts" :key="product.id" class="bg-white rounded-2xl border border-slate-100 overflow-hidden shadow-sm hover:shadow-md transition-shadow flex flex-col justify-between">
          <div>
            <div class="relative aspect-[4/3] overflow-hidden bg-slate-100">
              <span v-if="product.tag" class="absolute top-3 left-3 z-10 bg-rose-800 text-white text-xs font-bold px-2.5 py-1 rounded">{{ product.tag }}</span>
              <img :src="product.image" class="w-full h-full object-cover" :alt="product.title" />
            </div>
            <div class="p-4 space-y-2">
              <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1">{{ product.title }}</h3>
            </div>
          </div>
          <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <div>
              <span class="text-base font-extrabold text-rose-950">৳ {{ product.price }}</span>
              <span class="text-xs text-slate-400 line-through ml-1.5">৳ {{ product.originalPrice }}</span>
            </div>
            <button @click="selectedProduct = product" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3 py-1.5 rounded-lg transition-colors">
              দ্রুত দেখুন
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- 9. The Making Process (Step-by-Step) -->
    <section class="space-y-10">
      <div class="text-center max-w-xl mx-auto space-y-2">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">আমাদের প্রক্রিয়া</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">যেভাবে তৈরি হয় একেকটি শিল্পকর্ম</h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
        <div v-for="(step, i) in [
          { step: '০১', title: 'কাপড় নির্বাচন', desc: 'শীত ও গরমের উপযোগী শতভাগ প্রি-ওয়াশড সুতি কাপড় বাছা হয়।' },
          { step: '০২', title: 'আঁকা ও নকশা', desc: 'অভিজ্ঞ শিল্পীদের হাতে ঐতিহ্যবাহী ফুল, লতা ও পাখির মোটিফ আঁকা হয়।' },
          { step: '০৩', title: 'হাতে সেলাই', desc: 'শত শত ঘণ্টার নিখুঁত ফোঁড়ে ফোঁড়ে তৈরি হয় মনের মতো নকশা।' },
          { step: '০৪', title: 'ফাইনাল ওয়াশ ও চেক', desc: 'গুণগত মান যাচাই ও ফিনিশিং শেষে আপনার ঠিকানায় ডেলিভারি।' }
        ]" :key="i" class="p-6 bg-white rounded-2xl border border-slate-100 shadow-sm relative space-y-3">
          <span class="text-3xl font-extrabold font-serif text-rose-900/20 absolute top-4 right-4">{{ step.step }}</span>
          <h3 class="font-bold text-lg font-serif text-slate-900">{{ step.title }}</h3>
          <p class="text-xs text-slate-600 leading-relaxed">{{ step.desc }}</p>
        </div>
      </div>
    </section>

    <!-- 10. Customer Testimonials -->
    <section class="bg-slate-50 rounded-3xl p-8 sm:p-12 space-y-8">
      <div class="text-center max-w-xl mx-auto space-y-2">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">গ্রাহক মতামত</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">আমাদের ক্রেতারা যা বলছেন</h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div v-for="(review, i) in [
          { name: 'ফারজানা আক্তার', location: 'ঢাকা', text: 'ডাবল কাঁথাটি হাতে পাওয়ার পর মুগ্ধ হয়ে গেছি! সেলাইয়ের ফোঁড়গুলো এত নিখুঁত আর কালার একদম পাকা।' },
          { name: 'তাসনিয়া আহমেদ', location: 'চট্টগ্রাম', text: 'বেবি কাঁথার কম্বোটা নিয়েছি নবজাতকের জন্য। কাপড়টা অসম্ভব নরম ও আরামদায়ক।' },
          { name: 'মাহমুদুল হাসান', location: 'সিলেট', text: 'মাকে উপহার দিয়েছিলাম ঐতিহ্যবাহী শাপলা কাঁথাটি। মা খুব খুশি হয়েছেন। ধন্যবাদ এমন সুন্দর কাজের জন্য।' }
        ]" :key="i" class="bg-white p-6 rounded-2xl border border-slate-200/60 shadow-sm space-y-4">
          <div class="flex text-amber-400 text-sm">★★★★★</div>
          <p class="text-sm text-slate-600 italic">"{{ review.text }}"</p>
          <div class="border-t border-slate-100 pt-3 flex justify-between items-center text-xs">
            <span class="font-bold text-slate-900">{{ review.name }}</span>
            <span class="text-slate-400">{{ review.location }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 11. Limited-Time Offer Banner -->
    <section class="bg-gradient-to-r from-rose-900 to-rose-950 text-white rounded-3xl p-8 sm:p-12 flex flex-col md:flex-row items-center justify-between gap-8">
      <div class="space-y-3 max-w-xl">
        <span class="bg-amber-400 text-slate-950 font-bold text-xs px-3 py-1 rounded-full uppercase">বিশেষ অফার</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif">চলমান শীতে আপনার ঘরের উষ্ণতা বাড়াতে</h2>
        <p class="text-rose-100 text-sm">যেকোনো ডাবল নকশী কাঁথা অর্ডারে পাচ্ছেন ফ্রি হোম ডেলিভারি ও আকর্ষণীয় কুপন ছাড়!</p>
      </div>
      <button class="bg-amber-400 hover:bg-amber-300 text-slate-950 font-bold px-8 py-3.5 rounded-xl shadow-lg transition-colors whitespace-nowrap">
        অর্ডার করুন এখনি 🛍️
      </button>
    </section>

    <!-- 12. Why Choose Us (Comparison) -->
    <section class="space-y-8">
      <div class="text-center max-w-xl mx-auto space-y-2">
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">কেন আমাদের নকশী কাঁথা আলাদা?</h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto">
        <div class="p-6 bg-white rounded-2xl border border-rose-100 shadow-sm space-y-4">
          <h3 class="text-lg font-bold font-serif text-rose-900 flex items-center gap-2">✨ আমাদের ঐতিহ্যবাহী হস্তশিল্প</h3>
          <ul class="space-y-2 text-sm text-slate-700">
            <li>✔️ ১০০% জামালপুরের অভিজ্ঞ নারী কারিগরদের হাতে সেলাই</li>
            <li>✔️ প্রি-ওয়াশড পাকা সুতি কাপড় ও রং</li>
            <li>✔️ দীর্ঘস্থায়ী ও প্রজন্ম থেকে প্রজন্মে ব্যবহারের উপযোগী</li>
            <li>✔️ ক্যাশ অন ডেলিভারিতে চেক করার সুযোগ</li>
          </ul>
        </div>
        <div class="p-6 bg-slate-50 rounded-2xl border border-slate-200 shadow-sm space-y-4 opacity-75">
          <h3 class="text-lg font-bold font-serif text-slate-500 flex items-center gap-2">⚠️ সাধারণ মেশিন প্রিন্ট কাঁথা</h3>
          <ul class="space-y-2 text-sm text-slate-500">
            <li>❌ কারখানায় মেশিনে তৈরি রেপ্লিকা</li>
            <li>❌ অল্পদিনেই রং ফেকাশে হয়ে যাওয়া</li>
            <li>❌ পাতলা ও নিম্নমানের কাপড়</li>
            <li>❌ ডেলিভারির পর বদলানোর সুযোগ থাকে না</li>
          </ul>
        </div>
      </div>
    </section>

    <!-- 13. Instagram / Photo Gallery Grid -->
    <section class="space-y-6">
      <div class="text-center max-w-xl mx-auto space-y-2">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">সোশ্যাল গ্যালারি</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">গ্রাহকদের ঘরে আমাদের কাঁথা</h2>
      </div>
      <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
        <div v-for="(img, i) in [
          'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=400',
          'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=400',
          'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=400',
          'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=400'
        ]" :key="i" class="aspect-square rounded-2xl overflow-hidden group relative">
          <img :src="img" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300" alt="Gallery" />
        </div>
      </div>
    </section>

    <!-- 14. Custom Design Banner -->
    <section class="bg-amber-100/60 rounded-3xl p-8 sm:p-12 border border-amber-200 text-center space-y-4 max-w-3xl mx-auto">
      <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">নিজের পছন্দমতো রঙ ও নকশায় কাঁথা বানাতে চান?</h2>
      <p class="text-sm text-slate-700">আপনার পছন্দের কালার কম্বো বা মাপ জানিয়ে দিন। আমাদের কারিগররা আপনার মনের মতো করে তৈরি করে দেবেন।</p>
      <button class="bg-rose-900 hover:bg-rose-950 text-white font-bold text-sm px-6 py-3 rounded-xl transition-colors">
        কাস্টম অর্ডার করুন 📞
      </button>
    </section>

    <!-- 15. Artisan Spotlight -->
    <section class="grid lg:grid-cols-2 gap-10 items-center bg-white p-8 sm:p-12 rounded-3xl border border-slate-100 shadow-sm">
      <div class="rounded-2xl overflow-hidden aspect-[4/3]">
        <img src="https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=800" class="w-full h-full object-cover" alt="Artisan" />
      </div>
      <div class="space-y-4">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">কারিগর পরিচিতি</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">হাতের জাদুকর নারী কারিগরগণ</h2>
        <p class="text-sm text-slate-600 leading-relaxed">
          জামালপুরের মেলান্দহ ও মাদারগঞ্জ এলাকার শত শত গ্রামীণ নারী তাদের কুটির শিল্পের মাধ্যমে আজ স্বাবলম্বী। আপনার প্রতিটি ক্রয়ের একটি বড় অংশ সরাসরি এই দক্ষ শিল্পীদের জীবনমান উন্নয়নে ব্যয় হয়।
        </p>
      </div>
    </section>

    <!-- 16. FAQ Section (Custom Accordion) -->
    <section class="max-w-3xl mx-auto space-y-6">
      <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 text-center">সাধারণ কিছু প্রশ্নের উত্তর</h2>
      <div class="space-y-3">
        <div v-for="(faq, i) in faqs" :key="i" class="border border-slate-200 rounded-xl overflow-hidden bg-white">
          <button
            @click="activeFaq = activeFaq === i ? null : i"
            class="w-full text-left p-5 font-bold font-serif text-slate-800 flex justify-between items-center"
          >
            <span>{{ faq.q }}</span>
            <span>{{ activeFaq === i ? '−' : '+' }}</span>
          </button>
          <div v-if="activeFaq === i" class="p-5 pt-0 text-sm text-slate-600 leading-relaxed border-t border-slate-50">
            {{ faq.a }}
          </div>
        </div>
      </div>
    </section>

    <!-- 17. Newsletter Signup -->
    <section class="bg-rose-950 text-white rounded-3xl p-8 sm:p-12 text-center space-y-6 max-w-4xl mx-auto">
      <h2 class="text-2xl sm:text-3xl font-bold font-serif">নতুন ডিজাইন ও অফার সবার আগে পেতে সাবস্ক্রাইব করুন</h2>
      <div class="flex flex-col sm:flex-row gap-3 max-w-md mx-auto">
        <input type="email" placeholder="আপনার ইমেইল ঠিকানা লিখুন" class="px-4 py-3 rounded-xl bg-white/10 border border-white/20 text-white placeholder-rose-200/60 text-sm focus:outline-none flex-1" />
        <button class="bg-amber-400 text-slate-950 font-bold px-6 py-3 rounded-xl text-sm whitespace-nowrap">যুক্ত হোন</button>
      </div>
    </section>

    <!-- 18. Footer Trust & Security Bar -->
    <section class="border-t border-slate-200 pt-8 flex flex-col sm:flex-row items-center justify-between text-xs text-slate-500 gap-4">
      <p>© 2026 Nakshi Katha Studio. সর্বস্বত্ব সংরক্ষিত। জামালপুরের ঐতিহ্য।</p>
      <div class="flex gap-4">
        <span>🔒 নিরাপদ পেমেন্ট</span>
        <span>🚚 সারা দেশে ক্যাশ অন ডেলিভারি</span>
        <span>💬 ২৪/৭ সাপোর্ট</span>
      </div>
    </section>

    <!-- Custom Quick-View Modal -->
    <div v-if="selectedProduct" class="fixed inset-0 z-50 bg-slate-950/60 backdrop-blur-sm flex items-center justify-center p-4">
      <div class="bg-white rounded-2xl max-w-lg w-full p-6 space-y-4 relative">
        <button @click="selectedProduct = null" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 font-bold text-lg">✕</button>
        <h3 class="font-serif text-lg font-bold text-slate-900">{{ selectedProduct.title }}</h3>
        <img :src="selectedProduct.image" class="w-full aspect-video object-cover rounded-xl" :alt="selectedProduct.title" />
        <div class="flex justify-between items-center">
          <span class="text-xl font-extrabold text-rose-950">৳ {{ selectedProduct.price }}</span>
          <button class="bg-rose-900 text-white font-bold px-6 py-2.5 rounded-xl text-sm">কার্টে যোগ করুন 🛒</button>
        </div>
      </div>
    </div>

  </div>
</template>