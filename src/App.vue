<template>
  <!-- Header -->
  <header id="header" class="fixed w-full top-0 z-50 transition-all duration-300">
    <div class="container mx-auto px-6 py-4">
      <nav class="flex justify-between items-center">
        <div class="flex items-center space-x-3">
          <div class="w-12 h-12 bg-white rounded-xl flex items-center justify-center shadow-lg">
            <div class="text-3xl transform hover:scale-110 transition-transform">
              <img :src="branding.logo" />
            </div>
          </div>
          <div
            class="text-3xl font-black text-teal-400 tracking-tight hover:opacity-80 transition-opacity cursor-pointer">
            {{ branding.name }}
          </div>
        </div>
        <ul class="hidden md:flex space-x-8">
          <li v-for="item in navigation" :key="item.id">
            <a :href="item.href" class="hover:text-white transition font-medium text-teal-400">
              {{ item.label }}
            </a>
          </li>
          <li>
            <a href="#download"
              class="bg-white text-primary px-6 py-2 rounded-lg font-semibold hover:bg-white/90 transition shadow-lg">
              Download
            </a>
          </li>
        </ul>
        <button @click="toggleMobileMenu"
          class="md:hidden w-12 h-12 flex items-center justify-center bg-white/10 rounded-xl hover:bg-white/20 transition">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path v-if="!isMobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"></path>
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12">
            </path>
          </svg>
        </button>
      </nav>
      <!-- Mobile Menu -->
      <div v-show="isMobileMenuOpen"
        class="md:hidden absolute top-full left-0 w-full bg-gradient-to-br from-primary to-secondary backdrop-blur-lg">
        <ul class="py-4 px-6 space-y-4">
          <li v-for="item in navigation" :key="item.id">
            <a :href="item.href" @click="closeMobileMenu"
              class="block py-2 hover:translate-x-2 transition-transform font-medium">
              {{ item.label }}
            </a>
          </li>
          <li>
            <a href="#download" @click="closeMobileMenu"
              class="inline-block bg-white text-primary px-6 py-2 rounded-lg font-semibold hover:bg-white/90 transition shadow-lg">
              Download
            </a>
          </li>
        </ul>
      </div>
    </div>
  </header>

  <!-- Hero Section -->
  <section class="min-h-screen pt-32 pb-20 px-6 relative overflow-hidden">
    <div class="absolute inset-0 bg-gradient-to-br from-primary via-primary to-secondary opacity-10"></div>
    <div class="container mx-auto max-w-6xl relative">
      <div class="grid md:grid-cols-2 gap-12 items-center">
        <div class="text-left">
          <div
            class="inline-block bg-white/10 backdrop-blur-lg px-4 py-2 rounded-full text-sm font-medium mb-6 animate-fadeInUp opacity-0"
            style="animation-delay: 0.2s">
            {{ hero.badge }}
          </div>
          <h1 class="text-5xl md:text-7xl font-black leading-tight mb-6 opacity-0 animate-fadeInUp"
            style="animation-delay: 0.4s">
            {{ hero.title }}
          </h1>
          <p class="text-xl md:text-2xl mb-8 text-white/90 leading-relaxed opacity-0 animate-fadeInUp"
            style="animation-delay: 0.6s">
            {{ hero.description }}
          </p>
          <div class="flex flex-col sm:flex-row gap-4 mb-8 opacity-0 animate-fadeInUp" style="animation-delay: 0.8s">
            <a v-for="btn in hero.buttons" :key="btn.id" :href="btn.href" :class="btn.class">
              {{ btn.text }}
              <span v-if="btn.arrow" class="ml-2 group-hover:translate-x-1 inline-block transition-transform">→</span>
            </a>
          </div>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 opacity-0 animate-fadeInUp" style="animation-delay: 1s">
            <div v-for="stat in hero.stats" :key="stat.id" class="bg-white/10 backdrop-blur-lg p-4 rounded-xl">
              <div class="flex items-center gap-2">
                <span class="text-2xl">{{ stat.icon }}</span>
                <div>
                  <div class="font-bold text-xl">{{ stat.value }}</div>
                  <div class="text-white/70 text-sm">{{ stat.label }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="flex justify-center relative">
          <div class="absolute inset-0 bg-gradient-to-br from-primary to-secondary opacity-20 blur-3xl rounded-full">
          </div>
          <div class="relative animate-float opacity-0 animate-fadeInUp" style="animation-delay: 0.6s">
            <div class="w-72 h-[580px] bg-black rounded-[3rem] p-3 shadow-2xl relative">
              <div class="absolute inset-0 bg-gradient-to-br from-primary to-secondary opacity-10 rounded-[3rem]">
              </div>
              <div
                class="w-full h-full bg-gradient-to-br from-[#A17E3E] to-[#488686] rounded-[2.5rem] relative overflow-hidden backdrop-blur-xl">
                <img :src="hero.appImage" alt="Roam App Interface"
                  class="w-full h-full object-cover rounded-2xl shadow-lg">
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="absolute bottom-0 left-0 w-full h-32 bg-gradient-to-t from-[#A17E3E] to-transparent opacity-20"></div>
  </section>

  <!-- Features Section -->
  <section id="features" class="py-20 bg-white text-gray-800">
    <div class="container mx-auto px-6 max-w-6xl">
      <h2 class="text-4xl md:text-5xl font-black text-center mb-4">
        {{ features.title.before }} <span :class="features.title.highlightClass">{{ features.title.highlight }}</span>
      </h2>
      <p class="text-center text-gray-600 text-lg mb-16 max-w-2xl mx-auto">
        {{ features.subtitle }}
      </p>

      <div class="grid md:grid-cols-3 gap-8">
        <div v-for="feature in features.items" :key="feature.id" :class="feature.cardClass">
          <div class="text-5xl mb-4">{{ feature.icon }}</div>
          <h3 class="text-2xl font-bold mb-3" :class="feature.titleClass">{{ feature.title }}</h3>
          <p class="text-gray-700 leading-relaxed">{{ feature.description }}</p>
        </div>
      </div>
    </div>
  </section>

  <!-- How It Works -->
  <section id="how-it-works" class="py-20 bg-gradient-to-br from-gray-900 to-gray-800 text-white">
    <div class="container mx-auto px-6 max-w-6xl">
      <h2 class="text-4xl md:text-5xl font-black text-center mb-16">
        {{ howItWorks.title.before }} <span class="text-[#A17E3E]">{{ howItWorks.title.highlight }}</span> {{
          howItWorks.title.after }}
      </h2>

      <div class="grid md:grid-cols-2 gap-16">
        <div v-for="section in howItWorks.sections" :key="section.id">
          <div class="flex items-center gap-3 mb-8">
            <div class="text-4xl">{{ section.icon }}</div>
            <h3 class="text-3xl font-bold">{{ section.title }}</h3>
          </div>
          <div class="space-y-6">
            <div v-for="step in section.steps" :key="step.id" class="flex gap-4">
              <div
                :class="['flex-shrink-0 w-12 h-12 rounded-full flex items-center justify-center font-bold text-xl', step.badgeClass]">
                {{ step.number }}
              </div>
              <div>
                <h4 class="font-bold text-xl mb-2">{{ step.title }}</h4>
                <p class="text-gray-300">{{ step.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Testimonials -->
  <section class="py-20 bg-gradient-to-br from-gray-50 to-white text-black">
    <div class="container mx-auto px-6 max-w-6xl">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-black mb-4">
          {{ testimonials.title.before }} <span class="text-primary">{{ testimonials.title.highlight }}</span>
        </h2>
        <p class="text-gray-600 text-lg max-w-2xl mx-auto">
          {{ testimonials.subtitle }}
        </p>
      </div>

      <div class="grid md:grid-cols-3 gap-8">
        <div v-for="testimonial in testimonials.items" :key="testimonial.id"
          class="bg-white rounded-2xl p-8 shadow-lg hover:shadow-xl transition transform hover:-translate-y-1">
          <div class="flex items-center gap-4 mb-6">
            <div
              class="w-16 h-16 bg-gradient-to-br from-primary to-secondary rounded-full flex items-center justify-center text-2xl">
              {{ testimonial.avatar }}
            </div>
            <div>
              <h4 class="font-bold text-lg">{{ testimonial.name }}</h4>
              <p class="text-gray-600">{{ testimonial.role }}</p>
            </div>
          </div>
          <p class="text-gray-700 leading-relaxed mb-4">
            {{ testimonial.content }}
          </p>
          <div class="flex items-center gap-1 text-primary">
            {{ testimonial.rating }}
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Pricing -->
  <section id="pricing" class="py-20 bg-white text-gray-800">
    <div class="container mx-auto px-6 max-w-6xl">
      <h2 class="text-4xl md:text-5xl font-black text-center mb-4">
        {{ pricing.title.before }} <span class="text-[#A17E3E]">{{ pricing.title.highlight }}</span> {{
          pricing.title.after }}
      </h2>
      <p class="text-center text-gray-600 text-lg mb-16">
        {{ pricing.subtitle }}
      </p>

      <div class="grid md:grid-cols-2 gap-8 max-w-5xl mx-auto">
        <div v-for="plan in pricing.plans" :key="plan.id" :class="plan.cardClass">
          <div class="text-center mb-6">
            <div class="text-4xl mb-3">{{ plan.icon }}</div>
            <h3 class="text-2xl font-bold mb-2">{{ plan.name }}</h3>
            <div class="text-4xl font-black mb-2" :class="plan.priceClass">{{ plan.price }}</div>
            <p :class="plan.descriptionClass">{{ plan.description }}</p>
          </div>
          <ul class="space-y-3">
            <li v-for="(feature, index) in plan.features" :key="index" class="flex items-start gap-2">
              <span :class="plan.checkmarkClass">✓</span>
              <span>{{ feature }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- Download Section -->
  <section id="download" class="py-20 bg-gradient-to-br from-[#A17E3E] to-[#488686]">
    <div class="container mx-auto px-6 max-w-4xl text-center">
      <h2 class="text-4xl md:text-5xl font-black mb-6">
        {{ download.title }}
      </h2>
      <p class="text-xl md:text-2xl mb-12 text-white/90">
        {{ download.subtitle }}
      </p>

      <div class="flex flex-col sm:flex-row gap-6 justify-center mb-12">
        <a v-for="store in download.stores" :key="store.id" :href="store.href"
          class="bg-black text-white px-8 py-4 rounded-2xl flex items-center gap-4 hover:scale-105 transition transform shadow-2xl">
          <span class="text-4xl">
            <img :src="store.logo" :class="store.logoClass" alt="">
          </span>
          <div class="text-left">
            <div class="text-xs">{{ store.prefix }}</div>
            <div class="text-xl font-bold">{{ store.name }}</div>
          </div>
        </a>
      </div>

      <div class="flex flex-wrap justify-center gap-8 text-sm">
        <div v-for="badge in download.badges" :key="badge.id" class="flex items-center gap-2">
          <span class="text-2xl">{{ badge.icon }}</span>
          <span>{{ badge.text }}</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="py-20 bg-gray-50 text-black">
    <div class="container mx-auto px-6 max-w-6xl">
      <div class="grid md:grid-cols-2 gap-12">
        <div>
          <h2 class="text-4xl font-black mb-6">
            {{ contact.title.before }} <span class="text-primary">{{ contact.title.highlight }}</span>
          </h2>
          <p class="text-gray-600 text-lg mb-8">
            {{ contact.subtitle }}
          </p>
          <div class="space-y-6">
            <div v-for="info in contact.info" :key="info.id" class="flex items-start gap-4">
              <div class="w-12 h-12 bg-primary/10 rounded-xl flex items-center justify-center flex-shrink-0">
                <span class="text-2xl">{{ info.icon }}</span>
              </div>
              <div>
                <h3 class="font-bold text-lg mb-1">{{ info.title }}</h3>
                <p class="text-gray-600">{{ info.value }}</p>
              </div>
            </div>
          </div>
        </div>
        <div>
          <form @submit.prevent="handleSubmit" class="bg-white rounded-2xl p-8 shadow-xl">
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-2">Full Name</label>
              <input v-model="contactForm.name" type="text"
                class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition">
            </div>
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-2">Email Address</label>
              <input v-model="contactForm.email" type="email"
                class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition">
            </div>
            <div class="mb-6">
              <label class="block text-sm font-medium text-gray-700 mb-2">Message</label>
              <textarea v-model="contactForm.message" rows="4"
                class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition"></textarea>
            </div>
            <button type="submit"
              class="w-full bg-gradient-to-r from-primary to-secondary text-white font-bold py-4 rounded-xl hover:opacity-90 transition transform hover:scale-[0.99]">
              Send Message
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="bg-gray-900 text-white py-12">
    <div class="container mx-auto px-6 max-w-6xl">
      <div class="grid md:grid-cols-4 gap-8 mb-8">
        <div>
          <div class="flex items-center gap-2 mb-4">
            <span class="text-3xl">
              <img :src="footer.logo" class="w-14" alt="">
            </span>
            <span class="text-2xl font-bold">{{ footer.brandName }}</span>
          </div>
          <p class="text-gray-400">{{ footer.tagline }}</p>
        </div>
        <div v-for="column in footer.columns" :key="column.id">
          <h4 class="font-bold text-lg mb-4">{{ column.title }}</h4>
          <ul class="space-y-2 text-gray-400">
            <li v-for="link in column.links" :key="link.id">
              <a :href="link.href" class="hover:text-[#A17E3E] transition">{{ link.text }}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="border-t border-gray-800 pt-8 text-center text-gray-400">
        <p>&copy; {{ currentYear }} {{ footer.copyright }}</p>
        <p class="mt-2">{{ footer.contactEmail }} | {{ footer.contactPhone }}</p>
      </div>
    </div>
  </footer>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      isMobileMenuOpen: false,
      currentYear: new Date().getFullYear(),
      support: {},

      // Contact Form
      contactForm: {
        name: '',
        email: '',
        message: ''
      },

      // Branding
      branding: {
        name: 'Roam App',
        logo: 'assets/logo.svg'
      },

      // Navigation
      navigation: [
        { id: 1, label: 'Features', href: '#features' },
        { id: 2, label: 'How It Works', href: '#how-it-works' },
        { id: 3, label: 'Pricing', href: '#pricing' },
        { id: 4, label: 'Contact', href: '#contact' }
      ],

      // Hero Section
      hero: {
        badge: '🎉 Trusted by 100,000+ Users Nationwide',
        title: 'Towing Made Simple & Reliable',
        description: 'Connect with verified tow truck drivers instantly. Get transparent pricing, real-time tracking, and peace of mind.',
        appImage: 'assets/app.png',
        buttons: [
          {
            id: 1,
            text: 'Get Started Free',
            href: '#download',
            class: 'group bg-white text-primary px-8 py-4 rounded-xl text-lg font-bold shadow-2xl hover:scale-105 hover:shadow-xl transition transform text-center relative overflow-hidden',
            arrow: false
          },
          {
            id: 2,
            text: 'Watch Demo',
            href: '#how-it-works',
            class: 'group bg-white/10 backdrop-blur-lg border-2 border-white/20 px-8 py-4 rounded-xl text-lg font-bold hover:bg-white/20 transition text-center',
            arrow: true
          }
        ],
        stats: [
          { id: 1, icon: '⭐', value: '4.8/5', label: 'User Rating' },
          { id: 2, icon: '🚚', value: '10K+', label: 'Active Drivers' },
          { id: 3, icon: '⚡', value: '5 min', label: 'Avg Response' },
          { id: 4, icon: '🎯', value: '99%', label: 'Success Rate' }
        ]
      },

      // Features
      features: {
        title: {
          before: 'Why Choose',
          highlight: 'Roam App?',
          highlightClass: 'text-[#A17E3E]'
        },
        subtitle: 'The most comprehensive tow truck platform for both users and drivers',
        items: [
          {
            id: 1,
            icon: '💰',
            title: 'Negotiate Prices',
            description: 'Chat directly with drivers and agree on a fair price before service. No hidden fees or surprises.',
            cardClass: 'bg-gradient-to-br from-amber-50 to-amber-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#A17E3E]'
          },
          {
            id: 2,
            icon: '🗺️',
            title: 'Real-Time Navigation',
            description: 'Track your tow truck\'s location in real-time. Know exactly when help will arrive with live updates.',
            cardClass: 'bg-gradient-to-br from-teal-50 to-teal-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#488686]'
          },
          {
            id: 3,
            icon: '🎟️',
            title: 'Promo Codes',
            description: 'Save money with exclusive promo codes and special offers for both first-time and loyal users.',
            cardClass: 'bg-gradient-to-br from-yellow-50 to-yellow-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#A17E3E]'
          },
          {
            id: 4,
            icon: '👥',
            title: 'Driver Network',
            description: 'Drivers can hire other tow trucks when they need backup. Collaborate and grow your business.',
            cardClass: 'bg-gradient-to-br from-cyan-50 to-cyan-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#488686]'
          },
          {
            id: 5,
            icon: '⚡',
            title: 'Instant Matching',
            description: 'Get matched with nearby available drivers instantly. No waiting, no delays, just fast service.',
            cardClass: 'bg-gradient-to-br from-emerald-50 to-emerald-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#488686]'
          },
          {
            id: 6,
            icon: '⭐',
            title: 'Ratings & Reviews',
            description: 'Rate your experience and read reviews from other users. Trust and transparency guaranteed.',
            cardClass: 'bg-gradient-to-br from-stone-50 to-stone-100 p-8 rounded-3xl hover:scale-105 transition transform shadow-lg',
            titleClass: 'text-[#A17E3E]'
          }
        ]
      },

      // How It Works
      howItWorks: {
        title: {
          before: 'How',
          highlight: 'Roam App',
          after: 'Works'
        },
        sections: [
          {
            id: 1,
            icon: '👤',
            title: 'For Users',
            steps: [
              {
                id: 1,
                number: '1',
                title: 'Request a Tow',
                description: 'Enter your location and destination. Get instant quotes from nearby drivers.',
                badgeClass: 'bg-[#A17E3E]'
              },
              {
                id: 2,
                number: '2',
                title: 'Negotiate & Choose',
                description: 'Chat with drivers, negotiate prices, and select the best option for you.',
                badgeClass: 'bg-[#A17E3E]'
              },
              {
                id: 3,
                number: '3',
                title: 'Track & Relax',
                description: 'Track your driver in real-time and get updates every step of the way.',
                badgeClass: 'bg-[#A17E3E]'
              },
              {
                id: 4,
                number: '4',
                title: 'Pay & Rate',
                description: 'Secure payment through the app. Rate your experience and help others.',
                badgeClass: 'bg-[#A17E3E]'
              }
            ]
          },
          {
            id: 2,
            icon: '🚛',
            title: 'For Drivers',
            steps: [
              {
                id: 1,
                number: '1',
                title: 'Go Online',
                description: 'Turn on availability and start receiving tow requests in your area.',
                badgeClass: 'bg-[#488686]'
              },
              {
                id: 2,
                number: '2',
                title: 'Accept & Negotiate',
                description: 'Review requests, negotiate fair prices, and accept jobs that work for you.',
                badgeClass: 'bg-[#488686]'
              },
              {
                id: 3,
                number: '3',
                title: 'Navigate & Tow',
                description: 'Use built-in navigation to reach customers quickly and efficiently.',
                badgeClass: 'bg-[#488686]'
              },
              {
                id: 4,
                number: '4',
                title: 'Earn & Grow',
                description: 'Get paid instantly. Hire backup drivers when needed and expand your fleet.',
                badgeClass: 'bg-[#488686]'
              }
            ]
          }
        ]
      },

      // Testimonials
      testimonials: {
        title: {
          before: 'Loved by',
          highlight: 'Thousands'
        },
        subtitle: 'Join our community of satisfied users who have experienced the future of towing services',
        items: [
          {
            id: 1,
            avatar: '👨',
            name: 'Michael Thompson',
            role: 'Car Owner',
            content: 'Roam App saved me when my car broke down on the highway. Within minutes, I was connected with a driver, and the transparent pricing gave me peace of mind.',
            rating: '⭐⭐⭐⭐⭐'
          },
          {
            id: 2,
            avatar: '👩',
            name: 'Sarah Martinez',
            role: 'Tow Truck Driver',
            content: 'As a driver, Roam App has transformed my business. The platform is intuitive, payments are instant, and I can manage my fleet effortlessly.',
            rating: '⭐⭐⭐⭐⭐'
          },
          {
            id: 3,
            avatar: '🧑',
            name: 'Alex Chen',
            role: 'Business Owner',
            content: 'Running a delivery business, vehicle reliability is crucial. Roam App\'s quick response times and professional service keep our operations smooth.',
            rating: '⭐⭐⭐⭐⭐'
          }
        ]
      },

      // Pricing
      pricing: {
        title: {
          before: 'Simple,',
          highlight: 'Transparent',
          after: 'Pricing'
        },
        subtitle: 'No subscription fees. No hidden charges. Pay only for what you use.',
        plans: [
          {
            id: 1,
            icon: '👤',
            name: 'Users',
            price: 'FREE',
            description: 'Download & use',
            priceClass: 'text-[#A17E3E]',
            descriptionClass: 'text-gray-600',
            checkmarkClass: 'text-[#488686] text-xl',
            cardClass: 'border-2 border-gray-200 rounded-3xl p-8 hover:border-[#A17E3E] hover:shadow-2xl transition',
            features: [
              'Unlimited tow requests',
              'Real-time tracking',
              'Price negotiation',
              'Promo codes'
            ]
          },
          {
            id: 2,
            icon: '🚛',
            name: 'Basic Driver',
            price: '',
            description: 'Commission per job',
            priceClass: '',
            descriptionClass: '',
            checkmarkClass: 'text-xl',
            cardClass: 'bg-gradient-to-br from-[#A17E3E] to-[#488686] text-white rounded-3xl p-8 transform scale-105 shadow-2xl',
            features: [
              'Unlimited job requests',
              'Hire other drivers',
              'Instant payments',
              'Navigation tools',
              'Customer support'
            ]
          }
        ]
      },

      // Download
      download: {
        title: 'Ready to Get Started?',
        subtitle: 'Download Roam App today and experience the future of towing services',
        stores: [
          {
            id: 1,
            href: '#',
            logo: 'assets/apple.png',
            logoClass: 'w-14',
            prefix: 'Download on the',
            name: 'App Store'
          },
          {
            id: 2,
            href: '#',
            logo: 'assets/play-store.png',
            logoClass: 'w-10',
            prefix: 'Get it on',
            name: 'Google Play'
          }
        ],
        badges: [
          { id: 1, icon: '🔒', text: 'Secure & Safe' },
          { id: 2, icon: '⚡', text: 'Fast Setup' },
          { id: 3, icon: '💯', text: '100% Free' }
        ]
      },
    };
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
    },
    closeMobileMenu() {
      this.isMobileMenuOpen = false;
    },
    async handleSubmit() {
      await axios.post(import.meta.env.VITE_SERVER_URL + '/contact', this.contactForm);
      alert('Thank you for your message! We\'ll get back to you soon.');
    }
  },
  async mounted() {
    // set dynamic data
    const res = await axios.get(import.meta.env.VITE_SERVER_URL + '/setting/support');
    this.support = res?.data?.data?.value;

    // Header scroll effect
    let ticking = false;
    const header = document.getElementById('header');

    const updateHeader = () => {
      if (window.scrollY > 50) {
        header.classList.add('glass-effect', 'shadow-lg');
      } else {
        header.classList.remove('glass-effect', 'shadow-lg');
      }
      ticking = false;
    };

    window.addEventListener('scroll', () => {
      if (!ticking) {
        window.requestAnimationFrame(updateHeader);
        ticking = true;
      }
    });

    // Smooth scrolling
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        const href = this.getAttribute('href');
        if (href !== '#') {
          e.preventDefault();
          const target = document.querySelector(href);
          if (target) {
            const headerOffset = 100;
            const elementPosition = target.getBoundingClientRect().top;
            const offsetPosition = elementPosition + window.pageYOffset - headerOffset;

            window.scrollTo({
              top: offsetPosition,
              behavior: 'smooth'
            });
          }
        }
      });
    });

    // Reveal animations on scroll
    const observerOptions = {
      root: null,
      rootMargin: '0px',
      threshold: 0.1
    };

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.remove('opacity-0');
          observer.unobserve(entry.target);
        }
      });
    }, observerOptions);

    document.querySelectorAll('.animate-fadeInUp').forEach(el => {
      observer.observe(el);
    });
  },
  computed: {
    footer() {
      return {
        logo: 'assets/logo.svg',
        brandName: 'Roam',
        tagline: 'Making towing simple, fast, and affordable for everyone.',
        copyright: 'Roam App. All rights reserved.',
        contactEmail: this.support?.email || 'N/A',
        contactPhone: this.support?.phone || 'N/A',
        columns: [
          {
            id: 1,
            title: 'Product',
            links: [
              { id: 1, text: 'Features', href: '#features' },
              { id: 2, text: 'Pricing', href: '#pricing' },
              { id: 3, text: 'FAQ', href: '#' }
            ]
          },
          {
            id: 2,
            title: 'Company',
            links: [
              { id: 1, text: 'About Us', href: '#' },
              { id: 2, text: 'Careers', href: '#' },
              { id: 3, text: 'Contact', href: '#' }
            ]
          },
          {
            id: 3,
            title: 'Legal',
            links: [
              { id: 1, text: 'Privacy Policy', href: '#' },
              { id: 2, text: 'Terms of Service', href: '#' },
              { id: 3, text: 'Cookie Policy', href: '#' }
            ]
          }
        ]
      }
    },
    contact() {
      return {
        title: {
          before: 'Let\'s Get in',
          highlight: 'Touch'
        },
        subtitle: 'Have questions or feedback? We\'d love to hear from you. Our team is here to help.',
        info: [
          {
            id: 1,
            icon: '📍',
            title: 'Office Location',
            value: this.support?.officeAddress || 'N/A'
          },
          {
            id: 2,
            icon: '📞',
            title: 'Phone Number',
            value: this.support?.phone || 'N/A'
          },
          {
            id: 3,
            icon: '✉️',
            title: 'Email Address',
            value: this.support?.email || 'N/A'
          }
        ]
      }
    },
  },
};
</script>
