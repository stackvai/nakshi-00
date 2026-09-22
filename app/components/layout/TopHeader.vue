<!-- components/layout/TopHeader.vue -->
<template>
  <div class="bg-rose-950 text-rose-100 text-xs sm:text-sm py-2 px-4 border-b border-rose-900/50">
    <div class="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-2">
      <!-- Announcement -->
      <div class="flex items-center gap-2 text-center sm:text-left">
        <span class="inline-block w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
        <p class="font-medium">
          সারাদেশে ফ্রি হোম ডেলিভারি! ১০০% খাঁটি হাতে তৈরি নকশী কাঁথা।
        </p>
      </div>

      <!-- Quick Contact Info -->
      <div class="flex items-center gap-4 text-xs">
        <a href="tel:+8801700000000" class="hover:text-amber-300 transition-colors flex items-center gap-1">
          <span>📞</span> +৮৮০ ১৭০০-০০০০০
        </a>
        <span class="text-rose-800">|</span>
        <NuxtLink to="/track-order" class="hover:text-amber-300 transition-colors">
          অর্ডার ট্র্যাক করুন
        </NuxtLink>
      </div>
    </div>
  </div>
</template>