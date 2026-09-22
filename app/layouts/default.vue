<!-- layouts/default.vue -->
<script setup lang="ts">
// JSON-LD Schema for E-Commerce Store
useHead({
  script: [
    {
      type: 'application/ld+json',
      children: JSON.stringify({
        '@context': 'https://schema.org',
        '@type': 'Store',
        'name': 'নকশী কাঁথা',
        'image': 'https://nakshikatha.com/logo.png',
        'description': 'বাংলাদেশের ঐতিহ্যবাহী হাতে সেলাই করা প্রিমিয়াম নকশী কাঁথা ও হস্তশিল্পের অনলাইন শপ।',
        'priceRange': '৳৳',
        'address': {
          '@type': 'PostalAddress',
          'addressCountry': 'BD',
          'addressLocality': 'Dhaka'
        }
      })
    }
  ]
})
</script>

<template>
  <div class="flex flex-col min-h-screen">
    <!-- Top Announcement Bar -->
    <LayoutTopHeader />

    <!-- Main Navigation Header -->
    <LayoutHeader />

    <!-- Categories & Navigation SubHeader -->
    <LayoutSubHeader />

    <!-- Page Body -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">
      <slot />
    </main>

    <!-- Footer -->
    <LayoutFooter />
  </div>
</template>