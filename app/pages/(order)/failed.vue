<!-- pages/checkout/failed.vue -->
<script setup lang="ts">
useHead({
  title: 'অর্ডার বা পেমেন্ট ব্যর্থ হয়েছে — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'আপনার অর্ডার প্রসেসিং বা অনলাইন পেমেন্ট সম্পন্ন করা সম্ভব হয়নি।' }
  ]
})
</script>

<template>
  <div class="max-w-lg mx-auto px-4 py-16 sm:py-24 text-center">
    
    <div class="bg-white/90 backdrop-blur-2xl p-8 sm:p-12 rounded-3xl border border-slate-200/80 shadow-2xl shadow-rose-950/5 space-y-6 relative overflow-hidden">
      
      <!-- Ambient Glow -->
      <div class="absolute top-0 right-0 w-32 h-32 bg-rose-500/10 rounded-bl-full pointer-events-none"></div>

      <!-- Failed Icon -->
      <div class="w-20 h-20 bg-rose-100 text-rose-600 rounded-full flex items-center justify-center text-4xl mx-auto shadow-inner">
        ✕
      </div>

      <!-- Header Content -->
      <div class="space-y-2">
        <span class="inline-block bg-rose-50 text-rose-800 border border-rose-200 text-xs font-bold px-3.5 py-1 rounded-full uppercase tracking-widest">
          অর্ডার প্রক্রিয়ায় ত্রুটি
        </span>
        <h1 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">
          অর্ডার সম্পন্ন করা যায়নি!
        </h1>
        <p class="text-xs sm:text-sm text-slate-500 leading-relaxed">
          দুঃখিত, পেমেন্ট গেটওয়ে টাইমআউট অথবা নেটওয়ার্ক সমস্যার কারণে আপনার ট্রানজেকশনটি সম্পন্ন হয়নি। আপনার অ্যাকাউন্ট থেকে কোনো অর্থ কাটা হয়ে থাকলে স্বয়ংক্রয়ভাবে রিফান্ড হয়ে যাবে।
        </p>
      </div>

      <!-- Troubleshooting Checklist -->
      <div class="bg-slate-50 border border-slate-200/80 rounded-2xl p-4 text-xs text-slate-600 text-left space-y-2">
        <p class="font-bold text-slate-800">কেন এই সমস্যা হতে পারে?</p>
        <ul class="list-disc list-inside space-y-1 text-slate-500">
          <li>মোবাইল ব্যাংকিং বা পিন কোড দেওয়ার সময় অতিরিক্ত সময় নেওয়া।</li>
          <li>ইন্টারনেট কানেকশন সাময়িকভাবে বিচ্ছিন্ন হওয়া।</li>
          <li>কার্ডে পর্যাপ্ত ব্যালেন্স না থাকা।</li>
        </ul>
      </div>

      <!-- Action Buttons -->
      <div class="pt-2 flex flex-col sm:flex-row gap-3">
        <NuxtLink to="/checkout" class="flex-1 bg-rose-900 hover:bg-rose-950 text-white font-bold py-3.5 rounded-2xl text-xs transition-colors shadow-md text-center">
          পুনরায় চেকআউট করুন 🔄
        </NuxtLink>
        <NuxtLink to="/cart" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold py-3.5 rounded-2xl text-xs transition-colors text-center">
          কার্টে ফিরে যান 🛒
        </NuxtLink>
      </div>

    </div>

  </div>
</template>