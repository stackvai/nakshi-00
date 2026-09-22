<!-- pages/blogs/[slug].vue -->
<script setup lang="ts">
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const postSlug = String(route.params.slug) || 'jamalpur-nakshi-katha-gi-certification'

// Mock post data lookup (in real app, fetch based on postSlug)
const post = ref({
  title: 'জামালপুরের নকশী কাঁথার জিআই (GI) স্বীকৃতি ও আমাদের শেকড়ের গল্প',
  categoryLabel: 'ঐতিহ্য ও ইতিহাস',
  date: '১৮ সেপ্টেম্বর, ২০২৬',
  readTime: '৪ মিনিট পঠন',
  author: {
    name: 'আবদুল বাসেত',
    role: 'প্রতিষ্ঠাতা, নকশী কাঁথা স্টুডিও',
    avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?q=80&w=200'
  },
  image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=1200',
  content: `
    পৌরুষ বা যান্ত্রিকতার ভিড়ে আমাদের লোকশিল্পগুলো যখন হারিয়ে যেতে বসেছিল, ঠিক তখন জামালপুরের নকশী কাঁথার ভৌগোলিক নির্দেশক (GI) স্বীকৃতি আমাদের সংস্কৃতির জন্য এক বিরাট প্রাপ্তি। শত শত বছর ধরে ব্রহ্মপুত্র নদের তীরের গ্রামীণ নারীরা তাদের সুঁচ ও সুতোর ফোঁড়ে যে ইতিহাস বুনে আসছেন, আজ তা আন্তর্জাতিকভাবে স্বীকৃত।

    ### শেকড়ের টানে সুতোর বুনন
    নকশী কাঁথা কেবল শীতের রাতে গায়ে দেওয়ার চাদর নয়; এটি এক খণ্ড ক্যানভাস যেখানে একজন নারী তার জীবনের সুখ, দুঃখ, স্বপ্ন এবং পারিপার্শ্বিক প্রকৃতির রূপ ফুটিয়ে তোলেন। সুচ আর সুতোর এই মিতালীতে প্রতিটি ফোঁড়ে লুকিয়ে থাকে শিল্পীর আবেগ।

    > "যে কাঁথাটি আজ আপনার শোবার ঘরের শোভা বাড়াচ্ছে, তার পেছনে রয়েছে একজন গ্রামীণ নারীর দীর্ঘ এক সপ্তাহের নিপুণ সাধনা।"

    ### কেন জামালপুরের কাঁথা এত বিশেষ?
    ১. **শতভাগ হস্তশিল্প:** কোনো মেশিন প্রিন্ট বা কারখানার ছাঁচে তৈরি নয়, সম্পূর্ণ নিজ হাতে ফোঁড় তোলা হয়।
    ২. **প্রি-ওয়াশড সুতি:** বারবার ধোয়ার পরেও সুতার শক্তি ও কোমলতা বজায় থাকে।
    ৩. **পাকা রং:** প্রাকৃতিক ও নিরাপদ রঙ ব্যবহারের কারণে এর উজ্জ্বলতা চিরস্থায়ী হয়।

    আমাদের এই ঐতিহ্যকে টিকিয়ে রাখতে এবং প্রান্তিক নারী কারিগরদের জীবনমান উন্নত করতে আপনাদের প্রতিটি ক্রেই সবচেয়ে বড় ভূমিকা পালন করছে।
  `
})

// Related Posts
const relatedPosts = [
  {
    id: 2,
    title: 'রেহানা বেগমের গল্প: কুঁড়েঘরের বারান্দা থেকে বিশ্বদরবারে',
    slug: 'artisan-rehana-begum-story',
    categoryLabel: 'কারিগরদের গল্প',
    date: '১০ সেপ্টেম্বর, ২০২৬',
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600'
  },
  {
    id: 3,
    title: 'শীতের রাতে ওমের ছোঁয়া: কীভাবে নেবেন আপনার নকশী কাঁথার সঠিক যত্ন?',
    slug: 'how-to-care-for-nakshi-katha',
    categoryLabel: 'যত্ন ও পরিচর্যা',
    date: '২৫ আগস্ট, ২০২৬',
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600'
  }
]
</script>

<template>
  <div class="max-w-4xl mx-auto px-4 space-y-12 py-12">

    <!-- Breadcrumb -->
    <div class="text-xs text-slate-500 flex items-center gap-2">
      <NuxtLink to="/" class="hover:text-rose-900">হোম</NuxtLink>
      <span>/</span>
      <NuxtLink to="/blogs" class="hover:text-rose-900">ব্লগ</NuxtLink>
      <span>/</span>
      <span class="text-slate-900 font-medium truncate">{{ post.title }}</span>
    </div>

    <!-- 1. Article Header -->
    <section class="space-y-6 text-center max-w-3xl mx-auto">
      <div class="flex items-center justify-center gap-3 text-xs">
        <span class="bg-amber-100 text-amber-900 font-bold px-3 py-1 rounded-md">{{ post.categoryLabel }}</span>
        <span class="text-slate-400">{{ post.date }}</span>
        <span class="text-slate-300">•</span>
        <span class="text-slate-400">{{ post.readTime }}</span>
      </div>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        {{ post.title }}
      </h1>
      
      <!-- Author info -->
      <div class="flex items-center justify-center gap-3 pt-2">
        <img :src="post.author.avatar" class="w-10 h-10 rounded-full object-cover border border-slate-200" alt="Author" />
        <div class="text-left">
          <h4 class="font-bold text-xs sm:text-sm text-slate-900">{{ post.author.name }}</h4>
          <p class="text-[11px] text-slate-500">{{ post.author.role }}</p>
        </div>
      </div>
    </section>

    <!-- 2. Hero Banner Image -->
    <div class="aspect-[16/9] rounded-3xl overflow-hidden shadow-lg border border-slate-200/80 bg-slate-100">
      <img :src="post.image" class="w-full h-full object-cover" alt="Blog Feature" />
    </div>

    <!-- 3. Article Body Content -->
    <article class="bg-white p-8 sm:p-14 rounded-3xl border border-slate-200/80 shadow-sm space-y-6 text-slate-700 text-base leading-relaxed">
      <div class="space-y-4 prose prose-slate max-w-none">
        <p class="text-lg font-serif text-slate-800 leading-relaxed font-medium">
          {{ post.content.split('\n\n')[0] }}
        </p>
        <p>
          {{ post.content.split('\n\n')[1] }}
        </p>
        
        <!-- Highlight Pull Quote -->
        <blockquote class="border-l-4 border-rose-900 bg-rose-50/60 p-5 rounded-r-2xl italic font-serif text-slate-900 my-6">
          "যে কাঁথাটি আজ আপনার শোবার ঘরের শোভা বাড়াচ্ছে, তার পেছনে রয়েছে একজন গ্রামীণ নারীর দীর্ঘ এক সপ্তাহের নিপুণ সাধনা।"
        </blockquote>

        <p>
          {{ post.content.split('\n\n')[3] }}
        </p>
      </div>

      <!-- Social Share & Tags -->
      <div class="pt-8 border-t border-slate-100 flex flex-col sm:flex-row justify-between items-center gap-4 text-xs font-bold text-slate-700">
        <div class="flex items-center gap-2">
          <span>শেয়ার করুন:</span>
          <button class="px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200">ফেসবুক</button>
          <button class="px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200">টুইটার</button>
          <button class="px-3 py-1.5 rounded-lg bg-slate-100 hover:bg-slate-200">লিংক কপি</button>
        </div>
        <span class="text-rose-900 bg-rose-50 px-3 py-1.5 rounded-lg border border-rose-100">#নকশীকাঁথা #জামালপুর #ঐতিহ্য</span>
      </div>
    </article>

    <!-- 4. Related Articles Section -->
    <section class="space-y-6 pt-6">
      <div class="border-b border-slate-200 pb-3">
        <h2 class="text-2xl font-bold font-serif text-slate-900">আরও অন্যান্য গল্প পড়ুন</h2>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <div v-for="rel in relatedPosts" :key="rel.id" class="bg-white rounded-2xl border border-slate-200/80 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
          <div>
            <div class="aspect-[16/10] overflow-hidden bg-slate-100 relative">
              <span class="absolute top-3 left-3 z-10 bg-rose-900 text-white text-[10px] font-bold px-2.5 py-1 rounded">
                {{ rel.categoryLabel }}
              </span>
              <img :src="rel.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt="Related post" />
            </div>
            <div class="p-5 space-y-2">
              <span class="text-xs text-slate-400">{{ rel.date }}</span>
              <h3 class="font-bold text-base text-slate-900 font-serif leading-snug group-hover:text-rose-900 transition-colors line-clamp-2">
                {{ rel.title }}
              </h3>
            </div>
          </div>
          <div class="p-5 pt-0">
            <NuxtLink :to="`/blogs/${rel.slug}`" class="text-xs font-bold text-rose-900 hover:underline">
              বিস্তারিত পড়ুন →
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>