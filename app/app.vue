<!-- app.vue -->
<script setup lang="ts">
useHead({
  htmlAttrs: {
    lang: 'bn',
    dir: 'ltr',
  },
  titleTemplate: (titleChunk) => {
    return titleChunk 
      ? `${titleChunk} | নকশী কাঁথা - ঐতিহ্যবাহী হস্তশিল্প` 
      : 'নকশী কাঁথা - প্রিমিয়াম হাতে সেলাই করা খাঁটি নকশী কাঁথা অনলাইন শপ';
  },
  link: [
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' },
    { 
      rel: 'stylesheet', 
      href: 'https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&display=swap' 
    }
  ],
})

useSeoMeta({
  title: 'নকশী কাঁথা - প্রিমিয়াম হাতে সেলাই করা খাঁটি নকশী কাঁথা অনলাইন শপ',
  ogTitle: 'নকশী কাঁথা - ঐতিহ্যবাহী হাতে সেলাই করা নকশী কাঁথার বিশ্বস্ত ঠিকানা',
  description: 'খাঁটি হাতে সেলাই করা প্রিমিয়াম নকশী কাঁথা, বেডশীট ও ঐতিহ্যবাহী হস্তশিল্প কিনুন সরাসরি গ্রামীন কারিগরদের কাছ থেকে। সেরা মান ও দ্রুত হোম ডেলিভারি।',
  ogDescription: 'খাঁটি হাতে সেলাই করা প্রিমিয়াম নকশী কাঁথা, বেডশীট ও ঐতিহ্যবাহী হস্তশিল্প কিনুন সরাসরি গ্রামীন কারিগরদের কাছ থেকে।',
  ogImage: '/images/og-nakshi-katha.jpg',
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <div class="font-['Hind_Siliguri'] text-slate-800 bg-slate-50 min-h-screen antialiased selection:bg-rose-900 selection:text-white">
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>