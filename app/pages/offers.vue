<!-- pages/offers.vue -->
<script setup lang="ts">
import { ref } from 'vue'

useHead({
  title: 'বিশেষ অফার ও ডিসকাউন্ট — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'নকশী কাঁথা স্টুডিওর বিশেষ ছাড়, ফ্ল্যাশ সেল এবং কুপন কোড ব্যবহার করে সাশ্রয়ী মূল্যে প্রিমিয়াম হস্তশিল্প কিনুন।' }
  ]
})

// Active coupon copying state
const copiedCode = ref<string | null>(null)

const copyCoupon = (code: string) => {
  navigator.clipboard.writeText(code)
  copiedCode.value = code
  setTimeout(() => {
    copiedCode.value = null
  }, 2500)
}

// Promo Coupons Database
const coupons = [
  {
    code: 'WINTER500',
    discount: '৳ ৫০০ ছাড়',
    minSpend: 'ন্যূনতম কেনাকাটা ৳ ৩,০০০',
    desc: 'শীতকালীন স্পেশাল কালেকশনে ৫০০ টাকা ইনস্ট্যান্ট ডিসকাউন্ট।',
    bg: 'from-rose-900 to-rose-950'
  },
  {
    code: 'EID1000',
    discount: '৳ ১০০০ ছাড়',
    minSpend: 'ন্যূনতম কেনাকাটা ৳ ৬,০০০',
    desc: 'বড় ও মাস্টারপিস ডাবল কাঁথা অর্ডারে ১০০০ টাকা পর্যন্ত ছাড়।',
    bg: 'from-amber-800 to-amber-950'
  },
  {
    code: 'FREESHIP',
    discount: 'ফ্রি ডেলিভারি',
    minSpend: 'যেকোনো অর্ডারে প্রযোজ্য',
    desc: 'সারা বাংলাদেশে যেকোনো ঠিকানায় ফ্রি হোম ডেলিভারি উপভোগ করুন।',
    bg: 'from-slate-800 to-slate-950'
  }
]

// Discounted Flash Sale Products Database
const offerProducts = [
  {
    id: 1,
    title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)',
    price: 4500,
    originalPrice: 5500,
    discountBadge: '১০০০ টাকা ছাড়',
    rating: 5.0,
    reviews: 48,
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600'
  },
  {
    id: 3,
    title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)',
    price: 1850,
    originalPrice: 2300,
    discountBadge: '৪৫০ টাকা ছাড়',
    rating: 5.0,
    reviews: 29,
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600'
  },
  {
    id: 4,
    title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট',
    price: 3200,
    originalPrice: 3900,
    discountBadge: '৭০০ টাকা ছাড়',
    rating: 4.8,
    reviews: 19,
    image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600'
  }
]
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-16 py-12">

    <!-- 1. Header Section -->
    <section class="text-center max-w-3xl mx-auto space-y-4">
      <span class="inline-block bg-amber-100 text-amber-900 border border-amber-200 text-xs font-bold px-4 py-1.5 rounded-full uppercase tracking-widest shadow-sm">
        স্পেশাল ডিসকাউন্ট ও অফার
      </span>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        শীতকালীন মেগা সেল ও কুপন অফার
      </h1>
      <p class="text-slate-600 text-base sm:text-lg leading-relaxed">
        আমাদের জিআই সনদপ্রাপ্ত প্রিমিয়াম হস্তশিল্পে উপভোগ করুন আকর্ষণীয় মূল্যছাড় এবং ফ্রি ডেলিভারি সুবিধা।
      </p>
    </section>

    <!-- 2. Flash Sale Banner -->
    <section class="bg-gradient-to-r from-rose-950 via-rose-900 to-amber-900 text-white rounded-3xl p-8 sm:p-12 shadow-xl flex flex-col lg:flex-row items-center justify-between gap-8 relative overflow-hidden">
      <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#fbbf24_1px,transparent_1px)] [background-size:16px_16px]"></div>
      
      <div class="space-y-3 relative z-10 text-center lg:text-left max-w-xl">
        <span class="bg-amber-400 text-slate-950 text-xs font-bold px-3.5 py-1 rounded-full uppercase tracking-wider">
          সীমিত সময়ের ফ্ল্যাশ সেল ⏰
        </span>
        <h2 class="text-3xl sm:text-4xl font-bold font-serif leading-tight">
          শাহী নকশী কাঁথায় ২০% পর্যন্ত ফ্ল্যাট ডিসকাউন্ট
        </h2>
        <p class="text-rose-100 text-sm">
          জামালপুরের ঐতিহ্যবাহী কারিগরদের তৈরি প্রতিটি মাস্টারপিস অর্ডারে লুফে নিন এই বিশেষ ছাড়।
        </p>
      </div>

      <div class="relative z-10 shrink-0">
        <NuxtLink to="/shop" class="inline-block bg-amber-400 hover:bg-amber-300 text-slate-950 font-bold px-8 py-4 rounded-2xl text-sm transition-all shadow-lg">
          এখনই কেনাকাটা করুন 🛍️
        </NuxtLink>
      </div>
    </section>

    <!-- 3. Promo Coupons Grid -->
    <section class="space-y-6">
      <div class="border-b border-slate-200 pb-3">
        <h2 class="text-2xl font-bold font-serif text-slate-900">উপলব্ধ কুপন কোডসমূহ</h2>
        <p class="text-xs text-slate-500 mt-0.5">চেকআউট করার সময় কোডটি ব্যবহার করুন অথবা কপি করুন</p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div v-for="coupon in coupons" :key="coupon.code" :class="['rounded-3xl p-6 text-white bg-gradient-to-br shadow-md flex flex-col justify-between space-y-6 relative overflow-hidden', coupon.bg]">
          
          <div class="space-y-2">
            <span class="bg-white/20 backdrop-blur-md text-amber-300 text-xs font-bold px-3 py-1 rounded-full">
              {{ coupon.minSpend }}
            </span>
            <h3 class="text-2xl sm:text-3xl font-extrabold font-serif">{{ coupon.discount }}</h3>
            <p class="text-xs text-rose-100/90">{{ coupon.desc }}</p>
          </div>

          <div class="pt-4 border-t border-white/10 flex items-center justify-between">
            <code class="bg-slate-950/40 text-amber-300 font-mono font-bold px-3.5 py-2 rounded-xl text-xs tracking-wider">
              {{ coupon.code }}
            </code>
            <button 
              @click="copyCoupon(coupon.code)" 
              class="bg-white hover:bg-amber-400 text-slate-950 font-bold text-xs px-4 py-2.5 rounded-xl transition-colors shadow-sm"
            >
              {{ copiedCode === coupon.code ? 'কপি হয়েছে! ✓' : 'কোড কপি করুন 📋' }}
            </button>
          </div>

        </div>
      </div>
    </section>

    <!-- 4. Special Discounted Products Grid -->
    <section class="space-y-6 pt-4">
      <div class="border-b border-slate-200 pb-3">
        <h2 class="text-2xl font-bold font-serif text-slate-900">অফারভুক্ত সেরা পণ্যসমূহ</h2>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="product in offerProducts" :key="product.id" class="bg-white rounded-3xl border border-slate-200/85 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
          <div>
            <div class="relative aspect-[4/3] overflow-hidden bg-slate-100">
              <span class="absolute top-3 left-3 z-10 bg-rose-900 text-white text-xs font-bold px-3 py-1 rounded-md shadow">
                {{ product.discountBadge }}
              </span>
              <img :src="product.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" :alt="product.title" />
            </div>
            <div class="p-6 space-y-2">
              <div class="flex items-center gap-2 text-xs">
                <span class="text-amber-500 font-bold">★ {{ product.rating }}</span>
                <span class="text-slate-400">({{ product.reviews }} রিভিউ)</span>
              </div>
              <h3 class="font-bold text-base text-slate-900 font-serif leading-snug group-hover:text-rose-900 transition-colors">
                {{ product.title }}
              </h3>
            </div>
          </div>
          <div class="p-6 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <div>
              <span class="text-lg font-extrabold text-rose-950">৳ {{ product.price }}</span>
              <span class="text-xs text-slate-400 line-through ml-2">৳ {{ product.originalPrice }}</span>
            </div>
            <NuxtLink :to="`/products/${product.id}`" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-4 py-2.5 rounded-xl transition-colors shadow-sm">
              বিস্তারিত 🛒
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>