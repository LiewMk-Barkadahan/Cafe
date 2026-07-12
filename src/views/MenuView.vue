<script setup>
import { ref, watch, onMounted, onUnmounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { Icon } from '@iconify/vue'

const route = useRoute()
const router = useRouter()
const activeCategory = ref('silog')
const showBackToTop = ref(false)

const categories = [
  { id: 'silog', label: 'Silog Meals', icon: 'mdi:food' },
  { id: 'packages', label: 'Barkada Packages', icon: 'mdi:account-group' },
  { id: 'snacks', label: 'Snacks', icon: 'mdi:food-croissant' },
  { id: 'drinks', label: 'Drinks', icon: 'mdi:coffee' },
  { id: 'billiards', label: 'Billiards', icon: 'mdi:billiards' },
  { id: 'services', label: 'Services', icon: 'mdi:printer' }
]

const menu = {
  silog: {
    title: 'Silog Meals',
    subtitle: 'All-day breakfast, served with love',
    items: [
      { name: 'Tosilog', desc: 'Tapa, sinangag, at itlog', price: '85' },
      { name: 'Longsilog', desc: 'Longganisa, sinangag, at itlog', price: '80' },
      { name: 'Tapsilog', desc: 'Beef tapa, sinangag, at itlog', price: '90' },
      { name: 'Hotsilog', desc: 'Hotdog, sinangag, at itlog', price: '75' },
      { name: 'Bangsilog', desc: 'Bangus, sinangag, at itlog', price: '95' },
      { name: 'Chicksilog', desc: 'Chicken, sinangag, at itlog', price: '85' },
      { name: 'Spamsilog', desc: 'Spam, sinangag, at itlog', price: '100' },
      { name: 'Cornsilog', desc: 'Corned beef, sinangag, at itlog', price: '80' }
    ]
  },
  packages: null,
  snacks: {
    title: 'Snacks',
    subtitle: 'Quick bites for your cravings',
    items: [
      { name: 'Nachos', desc: 'Loaded with cheese and salsa', price: '75' },
      { name: 'French Fries', desc: 'Crispy golden fries', price: '60' },
      { name: 'Lumpia', desc: 'Deep-fried spring rolls (3 pcs)', price: '50' },
      { name: 'Siomai', desc: 'Steamed dumplings (4 pcs)', price: '65' },
      { name: 'Chicken Wings', desc: '6 pcs, choice of flavor', price: '120' },
      { name: 'Sisig', desc: 'Sizzling pork sisig', price: '110' }
    ]
  },
  drinks: {
    title: 'Drinks',
    subtitle: 'Refresh and unwind',
    items: [
      { name: 'Iced Coffee', desc: 'Classic cold brew', price: '55' },
      { name: 'Iced Chocolate', desc: 'Rich chocolate over ice', price: '60' },
      { name: 'Bottled Water', desc: '500ml', price: '20' },
      { name: 'Softdrinks', desc: 'Coke, Sprite, or Royal', price: '25' },
      { name: 'Juice', desc: 'Calamansi or Dalandan', price: '40' },
      { name: 'Green Tea', desc: 'Hot or iced', price: '50' },
      { name: 'Barkada Signature Mix', desc: 'Pitcher, refreshing & smooth, made for sharing', price: '199' }
    ]
  },
  billiards: {
    title: 'Billiards',
    subtitle: 'Available through Barkada Packages',
    items: [
      { name: 'Classic Package', desc: '1 Hour billiard play included', price: '250' },
      { name: 'Bonding Package', desc: '1 Hour billiard play included', price: '320' },
      { name: 'VIP Package', desc: '2 Hours billiard play included', price: '420' }
    ]
  },
  services: {
    title: 'Other Services',
    subtitle: 'We have you covered',
    items: [
      { name: 'Printing (B&W)', desc: 'Per page', price: '5' },
      { name: 'Printing (Color)', desc: 'Per page', price: '10' },
      { name: 'Photocopy', desc: 'Per page', price: '2' },
      { name: 'GCash Cash In', desc: 'Service fee applies', price: '—' },
      { name: 'GCash Cash Out', desc: 'Service fee applies', price: '—' },
      { name: 'Wi-Fi Access', desc: 'Free for customers', price: 'FREE' }
    ]
  }
}

const packages = [
  {
    name: 'Barkadahan Classic',
    badge: 'Most Popular',
    price: '250',
    groupPrice: '1,000',
    savings: '80',
    forPax: '4 pax',
    image: new URL('../assets/pkg-classic.jpg', import.meta.url).href,
    inclusions: [
      '1 Silog meal of choice',
      'Unlimited juice',
      '1 Hour billiard play',
      'Free extra rice'
    ],
    perfectFor: ['Barkada hangouts', 'Date nights', 'Family time']
  },
  {
    name: 'Barkadahan Bonding',
    badge: 'Best Value',
    price: '320',
    groupPrice: '1,280',
    savings: '150',
    forPax: '4-5 pax',
    image: new URL('../assets/pkg-bonding.jpg', import.meta.url).href,
    inclusions: [
      '1 Silog meal of choice',
      'Unlimited juice',
      '1 Hour billiard play',
      '1 Pitcher Barkada Mix',
      'Free extra rice',
      'Board games & card games'
    ],
    perfectFor: ['Date nights', 'Family time', 'Celebrations']
  },
  {
    name: 'Barkadahan VIP',
    badge: 'Full Experience',
    price: '420',
    groupPrice: '1,680',
    savings: '300',
    forPax: '4 pax',
    image: new URL('../assets/pkg-vip.jpg', import.meta.url).href,
    inclusions: [
      '1 Silog meal of choice',
      'Unlimited juice (3 hours)',
      '2 Hours billiard play',
      '2 Pitchers Barkada Signature Mix',
      'Free extra rice',
      'Priority booking slot'
    ],
    perfectFor: ['Barkada night', 'Birthday celebrations', 'Company get-together', 'Special occasions']
  }
]

function setCategory(id) {
  activeCategory.value = id
  router.replace({ query: { category: id } })
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleScroll() {
  showBackToTop.value = window.scrollY > 400
}

onMounted(() => {
  const q = route.query.category
  if (q && (menu[q] || q === 'packages')) {
    activeCategory.value = q
  }
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

watch(() => route.query.category, (val) => {
  if (val && (menu[val] || val === 'packages')) {
    activeCategory.value = val
  }
})
</script>

<template>
  <div class="menu-page">
    <!-- Hero -->
    <header class="menu-hero">
      <div class="menu-hero-bg"></div>
      <div class="hero-overlay"></div>
      <div class="hero-content animate-fade-in">
        <h1>Our Menu</h1>
        <p>Discover what we have in store for you</p>
      </div>
    </header>

    <!-- Body -->
    <section class="menu-body">
      <!-- Tabs -->
      <div class="tabs-wrapper">
        <div class="category-tabs">
          <button
            v-for="cat in categories"
            :key="cat.id"
            class="tab-btn"
            :class="{ active: activeCategory === cat.id }"
            @click="setCategory(cat.id)"
          >
            <Icon :icon="cat.icon" width="16" height="16" />
            <span class="tab-label">{{ cat.label }}</span>
          </button>
        </div>
      </div>

      <!-- Barkada Packages -->
      <div v-if="activeCategory === 'packages'" class="menu-section animate-fade-in" key="packages">
        <div class="menu-header">
          <h2>Barkada Packages</h2>
          <p>For groups who deserve more!</p>
        </div>

        <div class="packages-grid">
          <div
            v-for="(pkg, index) in packages"
            :key="pkg.name"
            class="package-card"
            :class="{ featured: pkg.badge === 'Most Popular' }"
            :style="`animation-delay: ${0.1 * index}s`"
          >
            <div class="pkg-image">
              <img :src="pkg.image" :alt="pkg.name" />
            </div>
            <div class="pkg-header">
              <span class="pkg-badge">{{ pkg.badge }}</span>
              <h3>{{ pkg.name }}</h3>
              <p class="pkg-pax">For {{ pkg.forPax }}</p>
            </div>

            <div class="pkg-pricing">
              <div class="pkg-price">
                <span class="currency">&#8369;</span>
                <span class="amount">{{ pkg.price }}</span>
                <span class="per">/head</span>
              </div>
              <div class="pkg-group">
                <span>Group of 4 = </span>
                <strong>&#8369;{{ pkg.groupPrice }}</strong>
                <span class="savings">Save ~&#8369;{{ pkg.savings }}</span>
              </div>
            </div>

            <div class="pkg-inclusions">
              <h4>Inclusions</h4>
              <ul>
                <li v-for="item in pkg.inclusions" :key="item">
                  <Icon icon="mdi:check-circle" width="16" height="16" class="check-icon" />
                  {{ item }}
                </li>
              </ul>
            </div>

            <div class="pkg-perfect">
              <h4>Perfect for</h4>
              <div class="tags">
                <span v-for="tag in pkg.perfectFor" :key="tag" class="tag">{{ tag }}</span>
              </div>
            </div>
          </div>
        </div>

        <div class="reserve-cta animate-fade-in">
          <Icon icon="mdi:phone" width="18" height="18" />
          <div>
            <strong>Reserve Now!</strong>
            <p>0966 179 4944 &middot; Limited slots daily &middot; Reservation recommended</p>
          </div>
        </div>
      </div>

      <!-- Regular menu sections -->
      <div v-else class="menu-section animate-fade-in" :key="activeCategory">
        <div class="menu-header">
          <h2>{{ menu[activeCategory].title }}</h2>
          <p>{{ menu[activeCategory].subtitle }}</p>
        </div>

        <div class="menu-list">
          <div
            v-for="(item, index) in menu[activeCategory].items"
            :key="item.name"
            class="menu-item"
            :style="`animation-delay: ${0.04 * index}s`"
          >
            <div class="item-info">
              <span class="item-name">{{ item.name }}</span>
              <span class="item-desc">{{ item.desc }}</span>
            </div>
            <div class="item-price">
              <span v-if="item.price === 'FREE'" class="free-badge">FREE</span>
              <span v-else-if="item.price === '—'" class="price-dash">Ask staff</span>
              <span v-else class="price">&#8369;{{ item.price }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-inner">
        <div class="footer-grid">
          <div class="footer-brand">
            <div class="footer-logo">
              <Icon icon="mdi:coffee" width="22" height="22" color="white" />
            </div>
            <strong>LiewMk Barkadahan Cafe</strong>
          </div>

          <div class="footer-info">
            <div class="footer-col">
              <h4>Hours</h4>
              <p>Mon - Sat: 7:00 AM - 9:00 PM</p>
              <p>Sunday: 8:00 AM - 8:00 PM</p>
            </div>
            <div class="footer-col">
              <h4>Location</h4>
              <p>Block E-11 Lot 6, Brgy. San Mateo</p>
              <p>Dasmari&ntilde;as City, Cavite</p>
              <p class="muted">Beside Samuel Paint Center</p>
            </div>
            <div class="footer-col">
              <h4>Contact</h4>
              <p>0966 179 4944</p>
              <p>GCash &middot; Wi-Fi free for dine-in</p>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <p>&copy; 2026 LiewMk Barkadahan Cafe. All rights reserved.</p>
        </div>
      </div>
    </footer>

    <!-- Back to top -->
    <Transition name="fade">
      <button v-if="showBackToTop" class="back-to-top" @click="scrollToTop" aria-label="Back to top">
        <Icon icon="mdi:chevron-up" width="20" height="20" />
      </button>
    </Transition>
  </div>
</template>

<style scoped>
.menu-page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Hero */
.menu-hero {
  position: relative;
  height: 30vh;
  min-height: 200px;
  background-image: url('../assets/bg.jpg');
  background-size: cover;
  background-position: center 40%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(62, 39, 35, 0.55) 0%,
    rgba(62, 39, 35, 0.75) 100%
  );
}

.hero-content {
  position: relative;
  z-index: 1;
  color: white;
}

.hero-content h1 {
  font-size: clamp(2rem, 4vw, 2.8rem);
  margin-bottom: 0.35rem;
  letter-spacing: -0.5px;
}

.hero-content p {
  font-size: 1rem;
  opacity: 0.8;
}

/* Body */
.menu-body {
  flex: 1;
  max-width: 720px;
  width: 100%;
  margin: 0 auto;
  padding: 0 1.25rem 4rem;
}

/* Tabs */
.tabs-wrapper {
  position: sticky;
  top: 60px;
  z-index: 50;
  padding: 1.25rem 0 0.75rem;
  background: var(--bg-color);
}

.category-tabs {
  display: flex;
  gap: 0.4rem;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;
  padding-bottom: 0.25rem;
}

.category-tabs::-webkit-scrollbar {
  display: none;
}

.tab-btn {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.5rem 0.95rem;
  border: 1.5px solid rgba(93, 64, 55, 0.1);
  border-radius: 20px;
  background: white;
  cursor: pointer;
  white-space: nowrap;
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--text-mid);
  transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
  flex-shrink: 0;
}

.tab-btn:hover {
  border-color: var(--primary-light);
  color: var(--primary-color);
}

.tab-btn.active {
  background: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
  box-shadow: 0 2px 10px rgba(93, 64, 55, 0.3);
  transform: scale(1.03);
}

/* Menu section */
.menu-section {
  padding-top: 0.5rem;
}

.menu-header {
  margin-bottom: 1.25rem;
}

.menu-header h2 {
  font-size: 1.35rem;
  color: var(--primary-dark);
  margin-bottom: 0.15rem;
}

.menu-header p {
  color: var(--text-muted);
  font-size: 0.88rem;
}

/* Menu list */
.menu-list {
  display: flex;
  flex-direction: column;
  background: white;
  border-radius: var(--radius-lg);
  border: 1px solid rgba(93, 64, 55, 0.06);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
}

.menu-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.9rem 1.25rem;
  gap: 1rem;
  transition: background 0.2s ease;
}

.menu-item:not(:last-child) {
  border-bottom: 1px solid rgba(93, 64, 55, 0.05);
}

.menu-item:hover {
  background: rgba(93, 64, 55, 0.015);
}

.item-info {
  display: flex;
  flex-direction: column;
  gap: 0.1rem;
  min-width: 0;
}

.item-name {
  font-size: 0.92rem;
  font-weight: 600;
  color: var(--text-dark);
}

.item-desc {
  font-size: 0.78rem;
  color: var(--text-muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.item-price {
  text-align: right;
  flex-shrink: 0;
}

.price {
  font-size: 1rem;
  font-weight: 700;
  color: var(--primary-color);
  font-variant-numeric: tabular-nums;
}

.free-badge {
  font-size: 0.7rem;
  font-weight: 700;
  color: #2e7d32;
  background: #e8f5e9;
  padding: 0.2rem 0.55rem;
  border-radius: 10px;
  letter-spacing: 0.3px;
}

.price-dash {
  font-size: 0.78rem;
  color: var(--text-muted);
  font-style: italic;
}

/* Packages */
.packages-grid {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.package-card {
  background: white;
  border-radius: var(--radius-lg);
  border: 1px solid rgba(93, 64, 55, 0.06);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  padding: 1.5rem;
}

.package-card.featured {
  border-color: var(--accent-color);
  box-shadow: 0 2px 16px rgba(255, 183, 77, 0.15);
}

.pkg-header {
  margin-bottom: 1rem;
}

.pkg-badge {
  display: inline-block;
  font-size: 0.68rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 0.2rem 0.6rem;
  border-radius: 10px;
  background: var(--accent-light);
  color: #e65100;
  margin-bottom: 0.5rem;
}

.pkg-image {
  width: 100%;
  aspect-ratio: 1;
  border-radius: var(--radius-md);
  overflow: hidden;
  margin-bottom: 1rem;
}

.pkg-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.package-card.featured .pkg-badge {
  background: var(--accent-color);
  color: white;
}

.pkg-header h3 {
  font-size: 1.15rem;
  color: var(--primary-dark);
  margin-bottom: 0.15rem;
}

.pkg-pax {
  font-size: 0.82rem;
  color: var(--text-muted);
}

.pkg-pricing {
  background: rgba(93, 64, 55, 0.03);
  border-radius: var(--radius-md);
  padding: 1rem;
  margin-bottom: 1rem;
  text-align: center;
}

.pkg-price {
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 0.1rem;
  margin-bottom: 0.3rem;
}

.pkg-price .currency {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--primary-color);
}

.pkg-price .amount {
  font-size: 2.2rem;
  font-weight: 800;
  color: var(--primary-color);
  line-height: 1;
}

.pkg-price .per {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin-left: 0.15rem;
}

.pkg-group {
  font-size: 0.82rem;
  color: var(--text-mid);
}

.pkg-group strong {
  color: var(--primary-dark);
}

.savings {
  display: block;
  font-size: 0.75rem;
  color: #2e7d32;
  font-weight: 600;
  margin-top: 0.15rem;
}

.pkg-inclusions {
  margin-bottom: 1rem;
}

.pkg-inclusions h4,
.pkg-perfect h4 {
  font-size: 0.78rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  color: var(--text-muted);
  margin-bottom: 0.5rem;
}

.pkg-inclusions ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.pkg-inclusions li {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.85rem;
  color: var(--text-dark);
}

.check-icon {
  color: #2e7d32;
  flex-shrink: 0;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.35rem;
}

.tag {
  font-size: 0.72rem;
  font-weight: 500;
  padding: 0.2rem 0.55rem;
  border-radius: 10px;
  background: rgba(93, 64, 55, 0.06);
  color: var(--text-mid);
}

.reserve-cta {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-top: 1.5rem;
  padding: 1rem 1.25rem;
  background: var(--primary-dark);
  color: white;
  border-radius: var(--radius-lg);
  text-align: left;
}

.reserve-cta strong {
  font-size: 0.9rem;
  display: block;
  margin-bottom: 0.1rem;
}

.reserve-cta p {
  font-size: 0.78rem;
  opacity: 0.7;
}

/* Footer */
.footer {
  background: var(--primary-dark);
  color: rgba(255, 255, 255, 0.7);
  padding: 2.5rem 1.5rem 2rem;
  margin-top: auto;
}

.footer-inner {
  max-width: 960px;
  margin: 0 auto;
}

.footer-grid {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.footer-logo {
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.footer-brand strong {
  color: white;
  font-size: 0.95rem;
}

.footer-info {
  display: flex;
  gap: 2.5rem;
}

.footer-col h4 {
  color: white;
  font-size: 0.82rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 0.5rem;
}

.footer-col p {
  font-size: 0.8rem;
  line-height: 1.6;
  opacity: 0.7;
}

.footer-col .muted {
  opacity: 0.5;
  font-style: italic;
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1.25rem;
}

.footer-bottom p {
  font-size: 0.75rem;
  opacity: 0.4;
}


/* Back to top */
.back-to-top {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: none;
  background: var(--primary-color);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(93, 64, 55, 0.35);
  transition: all 0.25s cubic-bezier(0.22, 1, 0.36, 1);
  z-index: 90;
}

.back-to-top:hover {
  background: var(--primary-light);
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(93, 64, 55, 0.4);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(8px);
}

/* Responsive */
@media (max-width: 768px) {
  .footer-grid {
    flex-direction: column;
    gap: 1.5rem;
  }

  .footer-info {
    flex-direction: column;
    gap: 1.25rem;
  }
}

@media (max-width: 500px) {
  .menu-body {
    padding: 0 1rem 3rem;
  }

  .tab-btn {
    padding: 0.45rem 0.8rem;
    font-size: 0.76rem;
  }

  .menu-item {
    padding: 0.8rem 1rem;
  }

  .package-card {
    padding: 1.25rem;
  }

  .back-to-top {
    bottom: 1rem;
    right: 1rem;
  }
}
</style>
