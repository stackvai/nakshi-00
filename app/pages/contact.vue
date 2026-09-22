<!-- pages/contact.vue -->
<script setup lang="ts">
import { ref } from 'vue'

useHead({
  title: 'যোগাযোগ করুন — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'জামালপুরি জিআই সনদপ্রাপ্ত হস্তশিল্প ও নকশী কাঁথা অর্ডারের জন্য আমাদের সাথে যোগাযোগ করুন।' }
  ]
})

// Form state
const form = ref({
  name: '',
  phone: '',
  address: '',
  message: '',
  category: 'general'
})

const isSubmitting = ref(false)
const successMessage = ref(false)

const handleSubmit = () => {
  isSubmitting.value = true
  setTimeout(() => {
    isSubmitting.value = false
    successMessage.value = true
    form.value = { name: '', phone: '', address: '', message: '', category: 'general' }
    setTimeout(() => { successMessage.value = false }, 5000)
  }, 1200)
}

// FAQ State tracking active accordion per category
const activeFaqs = ref<{ [key: string]: number | null }>({
  general: 0, // Keep first open by default for rich interaction
  order: null,
  delivery: null,
  care: null
})

const toggleFaq = (category: string, index: number) => {
  activeFaqs.value[category] = activeFaqs.value[category] === index ? null : index
}

// 4 Separate FAQ categories with 7 questions each
const faqCategories = [
  {
    id: 'general',
    title: 'সাধারণ জিজ্ঞাসা ও ঐতিহ্য',
    faqs: [
      { q: 'আপনাদের নকশী কাঁথাগুলো কি সম্পূর্ণ হাতে সেলাই করা?', a: 'হ্যাঁ! আমাদের প্রতিটি পণ্য জামালপুরের অভিজ্ঞ নারী কারিগরদের দ্বারা শতভাগ নিজ হাতে সেলাই করা।' },
      { q: 'আপনাদের প্রতিষ্ঠান কি আসলেই জামালপুরের?', a: 'অবশ্যই। আমাদের মূল উৎপাদন কেন্দ্র জামালপুর সদর, মেলান্দহ ও মাদারগঞ্জ এলাকায় অবস্থিত।' },
      { q: 'নকশী কাঁথা ও সাধারণ কম্বলের মধ্যে পার্থক্য কী?', a: 'নকশী কাঁথা ঐতিহ্যবাহী হস্তশিল্প, যা সুতি কাপড় ও সুতার নিখুঁত ফোঁড়ে তৈরি হয়। এটি দেখতে নান্দনিক এবং ওমে আরামদায়ক।' },
      { q: 'আপনাদের কাঁথাগুলো কি জিআই (GI) সনদপ্রাপ্ত?', a: 'হ্যাঁ, জামালপুরের নকশী কাঁথা সরকারিভাবে ভৌগোলিক নির্দেশক বা জিআই সনদপ্রাপ্ত অরিজিনাল হস্তশিল্প।' },
      { q: 'পাইকারি বা বাল্ক অর্ডার নেওয়ার সুযোগ আছে কি?', a: 'হ্যাঁ, কর্পোরেট উপহার কিংবা পাইকারি অর্ডারের জন্য আপনারা আমাদের সাথে সরাসরি যোগাযোগ করতে পারেন।' },
      { q: 'আপনাদের সাথে সরাসরি কথা বলার মাধ্যম কী?', a: 'আপনারা আমাদের হটলাইন নম্বরে কল করতে পারেন অথবা এই পেজের ফর্ম ও ফেসবুক পেইজের মাধ্যমে মেসেজ পাঠাতে পারেন।' },
      { q: 'আপনাদের কাজের সাথে কি গ্রামীণ নারীরা যুক্ত আছেন?', a: 'হ্যাঁ, আমাদের সাথে ৬০০+ গ্রামীণ নারী কারিগর কাজ করছেন, যাঁদের উপার্জনের বড় মাধ্যম এই হস্তশিল্প।' }
    ]
  },
  {
    id: 'order',
    title: 'অর্ডার, পেমেন্ট ও কাস্টমাইজেশন',
    faqs: [
      { q: 'নিজের পছন্দমতো রঙ ও ডিজাইনে কাঁথা বানাতে পারব কি?', a: 'অবশ্যই! আপনার পছন্দের সাইজ, কালার কম্বো ও ডিজাইন জানিয়ে দিলে আমরা সে অনুযায়ী কাস্টম তৈরি করে দেব।' },
      { q: 'অর্ডার করার নিয়ম কী?', a: 'ওয়েবসাইট থেকে পছন্দসই পণ্যের নিচে "দ্রুত দেখুন" বা "কার্টে যোগ করুন" ক্লিক করে অথবা সরাসরি ফোন করে অর্ডার কনফার্ম করতে পারেন।' },
      { q: 'অগ্রিম পেমেন্ট কি বাধ্যতামূলক?', a: 'সাধারণত ক্যাশ অন ডেলিভারি দেওয়া হয়। তবে কাস্টম বা বিশেষ বড় অর্ডারের ক্ষেত্রে কিছু অগ্রিম প্রযোজ্য হতে পারে।' },
      { q: 'বিকাশ বা নগদের মাধ্যমে কি পেমেন্ট করা যাবে?', a: 'হ্যাঁ, আমাদের মার্চেন্ট বিকাশ, নগদ ও রকেট অ্যাকাউন্ট এবং অনলাইন ব্যাংকিংয়ের সুবিধা রয়েছে।' },
      { q: 'অর্ডার করার কতদিনের মধ্যে ডেলিভারি পাব?', a: 'স্টকে থাকা পণ্য সাধারণত ৩ থেকে ৫ দিনের মধ্যে দেশের যেকোনো প্রান্তে পৌঁছে যায়। কাস্টম অর্ডারে ৭-১০ দিন সময় লাগতে পারে।' },
      { q: 'অর্ডার কনফার্ম হওয়ার পর কি পরিবর্তন করা সম্ভব?', a: 'অর্ডার প্রসেসিংয়ে যাওয়ার আগে আমাদের কাস্টমার কেয়ারে যোগাযোগ করে পরিবর্তন করতে পারবেন।' },
      { q: 'গিফট বা উপহার দেওয়ার জন্য কি সুন্দর প্যাকেজিং পাওয়া যায়?', a: 'হ্যাঁ, উপহার দেওয়ার উপযোগী প্রিমিয়াম ও আকর্ষণীয় বক্স প্যাকেজিংয়ের ব্যবস্থা রয়েছে।' }
    ]
  },
  {
    id: 'delivery',
    title: 'ডেলিভারি ও শিপিং পলিসি',
    faqs: [
      { q: 'সারা বাংলাদেশে কি হোম ডেলিভারি দেওয়া হয়?', a: 'হ্যাঁ, আমরা বাংলাদেশের ৬৪ জেলায় কুরিয়ার সার্ভিসের মাধ্যমে হোম ডেলিভারি দিয়ে থাকি।' },
      { q: 'ডেলিভারির সময় পণ্য চেক করার সুযোগ আছে কি?', a: 'অবশ্যই! আমাদের ক্যাশ অন ডেলিভারি সুবিধায় কুরিয়ার ম্যানের সামনে পার্সেল খুলে পণ্য চেক করে তারপর পেমেন্ট করতে পারবেন।' },
      { q: 'ডেলিভারি চার্জ কত?', a: 'ঢাকা ও জামালপুর সদরের মধ্যে ডেলিভারি চার্জ তুলনামূলক কম, এবং অন্যান্য জেলায় স্ট্যান্ডার্ড কুরিয়ার চার্জ প্রযোজ্য।' },
      { q: 'পণ্য পাওয়ার পর পছন্দ না হলে কি রিটার্ন করা যাবে?', a: 'আমাদের প্রোডাক্টে কোনো ত্রুটি থাকলে বা বর্ণনা অনুযায়ী না মিললে ডেলিভারি ম্যানের সামনেই রিটার্ন করতে পারবেন।' },
      { q: 'জরুরি ভিত্তিতে একদিনের মধ্যে ডেলিভারি পাওয়া সম্ভব?', a: 'জরুরি প্রয়োজনের ক্ষেত্রে আমাদের সাথে ফোনে যোগাযোগ করলে ঢাকা ও জামালপুর এলাকায় বিশেষ ব্যবস্থায় পাঠানো সম্ভব।' },
      { q: 'পণ্য পাঠানোর পর ট্র্যাকিং করার ব্যবস্থা আছে কি?', a: 'হ্যাঁ, পার্সেল ডিসপ্যাচ হওয়ার পর আপনাকে কুরিয়ারের ট্র্যাকিং নম্বর বা আপডেট এসএমএস দিয়ে দেওয়া হবে।' },
      { q: 'প্রবাসীদের জন্য কি বিদেশে শিপিং করা হয়?', a: 'বর্তমানে প্রবাসী বাংলাদেশিদের অর্ডারের জন্য বিশেষ কুরিয়ার বা আত্মীয়দের ঠিকানায় পাঠানোর ব্যবস্থা রয়েছে।' }
    ]
  },
  {
    id: 'care',
    title: 'পণ্য পরিচর্যা ও ওয়াশ কেয়ার',
    faqs: [
      { q: 'নকশী কাঁথা কীভাবে ধুতে হবে?', a: 'হাতের তৈরি কাঁথাগুলো নরম ডিটারজেন্ট দিয়ে হালকা হাতে ধোয়া বা মৃদু ওয়াশিং মেশিনে ওয়াশ করা উত্তম।' },
      { q: 'ধোয়ার পর কি কাপড়ের রং উঠে যাবে?', a: 'একদমই না। আমরা ১০০% পাকা রঙের প্রি-ওয়াশড কটন সুতা ও সুতি কাপড় ব্যবহার করি।' },
      { q: 'কাঁথা রোদে শুকানো যাবে কি?', a: 'হালকা রোদে বা ছায়াযুক্ত স্থানে শুকানো ভালো। সরাসরি কড়া রোদে দীর্ঘক্ষণ না রাখাই শ্রেয়।' },
      { q: 'ইস্ত্রি করার নিয়ম কী?', a: 'মাঝারি তাপমাত্রায় (Medium heat) উল্টো দিক থেকে ইস্ত্রি করলে কাঁথার ফোঁড় ও সৌন্দর্য দীর্ঘদিন ঠিক থাকে।' },
      { q: 'দীর্ঘদিন ব্যবহারের পর কাঁথা কি নষ্ট হয়ে যায়?', a: 'সঠিক যত্ন নিলে আমাদের তৈরি নকশী কাঁথা প্রজন্ম থেকে প্রজন্মে নতুনের মতো টেকসই থাকে।' },
      { q: 'বেবি কাঁথার ক্ষেত্রে কি বিশেষ কোনো সতর্কতা মানতে হবে?', a: 'নবজাতকদের ত্বকের সুরক্ষায় বেবি কাঁথাগুলো মাইল্ড বেবি সোপ বা সাবান দিয়ে ধুয়ে রোদে শুকিয়ে নেওয়া উচিত।' },
      { q: 'দীর্ঘদিন না রাখলে কীভাবে সংরক্ষণ করতে হবে?', a: 'পরিষ্কার ও সম্পূর্ণ শুকানোর পর শুকনো ও বাতাস চলাচল করে এমন স্থানে ফোল্ড করে সংরক্ষণ করুন।' }
    ]
  }
]
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-28 lg:space-y-36 py-16 relative overflow-hidden">

    <!-- Decorative Animated Ambient Glows -->
    <div class="absolute top-10 left-1/2 -translate-x-1/2 w-[600px] h-[300px] bg-rose-200/40 rounded-full blur-3xl pointer-events-none -z-10 animate-pulse"></div>

    <!-- 1. Ultra-Modern Header Section -->
    <section class="text-center max-w-3xl mx-auto space-y-6">
      <div class="inline-flex items-center gap-2 bg-gradient-to-r from-amber-500/10 via-rose-500/10 to-amber-500/10 border border-amber-500/30 text-rose-900 text-xs font-bold px-4 py-2 rounded-full uppercase tracking-widest shadow-sm backdrop-blur-md">
        <span class="w-2 h-2 rounded-full bg-rose-800 animate-ping"></span>
        ২৪/৭ কাস্টমার সাপোর্ট ও যোগাযোগ
      </div>
      <h1 class="text-3xl sm:text-5xl lg:text-6xl font-extrabold font-serif text-slate-900 tracking-tight leading-tight">
        আপনার যেকোনো প্রশ্ন বা অর্ডারে আমরা আছি পাশে
      </h1>
      <p class="text-slate-600 text-base sm:text-lg leading-relaxed">
        জামালপুরের অরিজিনাল জিআই সনদপ্রাপ্ত নকশী কাঁথা কিংবা কাস্টম অর্ডারের বিষয়ে কথা বলতে নিচের মাধ্যমগুলোতে যোগাযোগ করুন।
      </p>
    </section>

    <!-- 2. Contact Cards & Interactive Form Section -->
    <section class="grid lg:grid-cols-3 gap-8 items-stretch">
      
      <!-- Contact Info Cards with Hover Elevate Effect -->
      <div class="space-y-6 lg:col-span-1 flex flex-col justify-between">
        
        <div class="p-6 sm:p-8 bg-white/80 backdrop-blur-xl rounded-3xl border border-slate-200/80 shadow-lg shadow-slate-100 hover:shadow-xl hover:-translate-y-1 transition-all duration-300 space-y-3 group">
          <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-rose-50 to-rose-100 text-rose-900 flex items-center justify-center text-2xl font-bold group-hover:scale-110 transition-transform shadow-inner">📞</div>
          <h3 class="font-bold text-lg font-serif text-slate-900">হটলাইন ও ফোন</h3>
          <p class="text-xs text-slate-500 leading-relaxed">যেকোনো প্রয়োজনে সরাসরি কল করুন:</p>
          <p class="text-base font-extrabold text-rose-950 tracking-wide">+৮৮০ ১৩০০-০০০০০০</p>
        </div>

        <div class="p-6 sm:p-8 bg-white/80 backdrop-blur-xl rounded-3xl border border-slate-200/80 shadow-lg shadow-slate-100 hover:shadow-xl hover:-translate-y-1 transition-all duration-300 space-y-3 group">
          <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-amber-50 to-amber-100 text-amber-900 flex items-center justify-center text-2xl font-bold group-hover:scale-110 transition-transform shadow-inner">📧</div>
          <h3 class="font-bold text-lg font-serif text-slate-900">ইমেইল ঠিকানা</h3>
          <p class="text-xs text-slate-500 leading-relaxed">অফিসিয়াল ইমেইল বা ক্যাটালগের জন্য:</p>
          <p class="text-sm font-bold text-slate-900">support@nakshikathastudio.com</p>
        </div>

        <div class="p-6 sm:p-8 bg-white/80 backdrop-blur-xl rounded-3xl border border-slate-200/80 shadow-lg shadow-slate-100 hover:shadow-xl hover:-translate-y-1 transition-all duration-300 space-y-3 group">
          <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-emerald-50 to-emerald-100 text-emerald-900 flex items-center justify-center text-2xl font-bold group-hover:scale-110 transition-transform shadow-inner">📍</div>
          <h3 class="font-bold text-lg font-serif text-slate-900">আমাদের ঠিকানা</h3>
          <p class="text-xs text-slate-500 leading-relaxed">প্রধান কার্যালয় ও ওয়ার্কশপ:</p>
          <p class="text-sm font-bold text-slate-900">মেলান্দহ রোড, জামালপুর সদর, জামালপুর, বাংলাদেশ।</p>
        </div>

      </div>

      <!-- Advanced Animated Glassmorphism Contact Form -->
      <div class="bg-white/90 backdrop-blur-2xl p-8 sm:p-12 rounded-3xl border border-slate-200/80 shadow-2xl shadow-rose-950/5 lg:col-span-2 space-y-6 relative overflow-hidden">
        
        <div class="absolute top-0 right-0 w-40 h-40 bg-gradient-to-br from-rose-500/10 to-amber-500/10 rounded-bl-full pointer-events-none"></div>

        <div class="space-y-1">
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">আমাদের মেসেজ পাঠান</h2>
          <p class="text-xs sm:text-sm text-slate-500">আপনার নাম, ফোন নম্বর ও বার্তা লিখে পাঠিয়ে দিন। আমরা দ্রুত যোগাযোগ করব।</p>
        </div>

        <!-- Success Toast Alert with Smooth Transition -->
        <transition enter-active-class="transition duration-300 ease-out" enter-from-class="transform -translate-y-2 opacity-0" leave-active-class="transition duration-200 ease-in" leave-to-class="transform -translate-y-2 opacity-0">
          <div v-if="successMessage" class="p-4 bg-emerald-50 border border-emerald-200 text-emerald-800 text-sm rounded-2xl flex items-center gap-3 shadow-sm">
            <span class="text-xl">🎉</span>
            <span>আপনার বার্তা সফলভাবে পাঠানো হয়েছে! খুব শীঘ্রই আমরা আপনার সাথে যোগাযোগ করব।</span>
          </div>
        </transition>

        <form @submit.prevent="handleSubmit" class="space-y-5">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
            <div class="space-y-2">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">আপনার নাম *</label>
              <input v-model="form.name" type="text" required placeholder="পুরো নাম লিখুন" class="w-full px-5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
            <div class="space-y-2">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">মোবাইল নম্বর *</label>
              <input v-model="form.phone" type="tel" required placeholder="01XXXXXXXXX" class="w-full px-5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
            <div class="space-y-2">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">ঠিকানা / জেলা</label>
              <input v-model="form.address" type="text" placeholder="যেমন: ধানমন্ডি, ঢাকা" class="w-full px-5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
            <div class="space-y-2">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">জিজ্ঞাসার বিষয়</label>
              <select v-model="form.category" class="w-full px-5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner cursor-pointer">
                <option value="general">সাধারণ তথ্য</option>
                <option value="order">নতুন বা কাস্টম অর্ডার</option>
                <option value="delivery">ডেলিভারি ও শিপিং</option>
                <option value="bulk">পাইকারি ক্রয়</option>
              </select>
            </div>
          </div>

          <div class="space-y-2">
            <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">আপনার বার্তা বিস্তারিত লিখুন *</label>
            <textarea v-model="form.message" rows="4" required placeholder="কোন সাইজ বা ডিজাইনের কাঁথা চাচ্ছেন তা এখানে লিখুন..." class="w-full px-5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner resize-none"></textarea>
          </div>

          <button type="submit" :disabled="isSubmitting" class="w-full bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-4 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2">
            <span v-if="isSubmitting" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
            {{ isSubmitting ? 'প্রসেসিং হচ্ছে...' : 'বার্তা পাঠান 🚀' }}
          </button>
        </form>
      </div>

    </section>

    <!-- 3. Comprehensive FAQs Section (4 Separate Categories with Animated Accordions) -->
    <section class="space-y-16 pt-12 border-t border-slate-200/80">
      
      <div class="text-center max-w-2xl mx-auto space-y-3">
        <span class="inline-block text-xs font-bold text-rose-900 uppercase tracking-widest bg-rose-50 px-3.5 py-1.5 rounded-full border border-rose-100">
          প্রশ্নোত্তর গাইডলাইন
        </span>
        <h2 class="text-3xl sm:text-4xl font-bold font-serif text-slate-900">যেসব প্রশ্ন সচরাচর করা হয়ে থাকে</h2>
        <p class="text-sm text-slate-500">নিচে আপনার প্রয়োজনীয় ক্যাটাগরি থেকে বিস্তারিত প্রশ্নের উত্তর দেখে নিতে পারেন।</p>
      </div>

      <!-- Loop through the 4 FAQ Categories -->
      <div v-for="cat in faqCategories" :key="cat.id" class="space-y-6 bg-gradient-to-b from-slate-50/80 to-white p-6 sm:p-10 rounded-3xl border border-slate-200/60 shadow-sm">
        
        <div class="border-b border-slate-200/80 pb-4 flex items-center justify-between">
          <h3 class="text-xl sm:text-2xl font-bold font-serif text-slate-900 flex items-center gap-3">
            <span class="w-2.5 h-2.5 rounded-full bg-rose-900"></span>
            {{ cat.title }}
          </h3>
          <span class="text-xs text-slate-400 font-medium">৭টি প্রশ্ন</span>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div v-for="(faq, i) in cat.faqs" :key="i" class="border border-slate-200/80 rounded-2xl overflow-hidden bg-white shadow-sm hover:border-rose-200 transition-colors">
            <button
              @click="toggleFaq(cat.id, i)"
              class="w-full text-left p-4 sm:p-5 font-bold font-serif text-slate-800 flex justify-between items-center gap-4 text-sm sm:text-base group"
            >
              <span class="group-hover:text-rose-900 transition-colors">{{ faq.q }}</span>
              <span class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center text-rose-900 font-extrabold text-base shrink-0 group-hover:bg-rose-900 group-hover:text-white transition-all">
                {{ activeFaqs[cat.id] === i ? '−' : '+' }}
              </span>
            </button>
            
            <!-- Smooth Collapse Animation Wrapper -->
            <div v-show="activeFaqs[cat.id] === i" class="px-5 pb-5 text-xs sm:text-sm text-slate-600 leading-relaxed border-t border-slate-50 pt-3 animate-fadeIn">
              {{ faq.a }}
            </div>
          </div>
        </div>

      </div>

    </section>

  </div>
</template>

<style scoped>
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-4px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fadeIn {
  animation: fadeIn 0.25s ease-out forwards;
}
</style>