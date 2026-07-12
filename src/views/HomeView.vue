<script setup>
import { Icon } from '@iconify/vue'

const services = [
  { id: 1, title: 'Homemade Silog', desc: 'All-day breakfast silog meals to start your day right.', bg: '#fff3e0', icon: 'mdi:silverware-fork-knife', iconColor: '#e65100', menuCategory: 'silog' },
  { id: 2, title: 'Junior Billiards', desc: 'Relax and play a game with friends in a cozy setting.', bg: '#e8eaf6', icon: 'mdi:billiards', iconColor: '#283593', menuCategory: 'billiards' },
  { id: 3, title: 'Printing Services', desc: 'Fast and reliable document printing for your needs.', bg: '#e0f2f1', icon: 'mdi:printer', iconColor: '#00695c', menuCategory: 'services' },
  { id: 4, title: 'GCash Services', desc: 'Convenient Cash In & Cash Out transactions.', bg: '#e3f2fd', icon: 'mdi:cash', iconColor: '#1565c0', menuCategory: 'services' },
  { id: 5, title: 'Snacks & Drinks', desc: 'Grab a quick bite and a refreshing drink while you chill.', bg: '#fce4ec', icon: 'mdi:food-fork-drink', iconColor: '#c62828', menuCategory: 'snacks' },
  { id: 6, title: 'Cozy Ambiance', desc: 'Quiet, cozy, and not crowded — your perfect hidden spot.', bg: '#e8f5e9', icon: 'mdi:leaf', iconColor: '#2e7d32', menuCategory: null }
]

const packages = [
  {
    name: 'Classic',
    price: '250',
    total: '1,000',
    image: new URL('../assets/pkg-classic.jpg', import.meta.url).href,
    inclusions: ['1 Silog meal of choice', 'Unlimited juice', '1 Hour billiard play', 'Free extra rice']
  },
  {
    name: 'Bonding',
    price: '320',
    total: '1,280',
    image: new URL('../assets/pkg-bonding.jpg', import.meta.url).href,
    inclusions: ['1 Silog meal of choice', 'Unlimited juice', '1 Hour billiard play', '1 Pitcher Barkada Mix', 'Free extra rice', 'Board & card games']
  },
  {
    name: 'VIP',
    price: '420',
    total: '1,680',
    image: new URL('../assets/pkg-vip.jpg', import.meta.url).href,
    inclusions: ['1 Silog meal of choice', 'Unlimited juice (3 hrs)', '2 Hours billiard play', '2 Pitchers Signature Mix', 'Free extra rice', 'Priority booking']
  }
]
</script>

<template>
  <div class="home">
    <!-- Hero -->
    <header class="hero">
      <div class="hero-bg"></div>
      <div class="hero-overlay"></div>
      <div class="hero-content animate-fade-in">
        <h1 class="hero-title">LiewMk Barkadahan Cafe</h1>
        <p class="hero-subtitle">Where great food meets good times and a cozy vibe.</p>
        <div class="hero-actions">
          <router-link to="/menu" class="cta-button primary">
            <span>View Menu</span>
            <Icon icon="mdi:arrow-right" width="18" height="18" />
          </router-link>
          <a href="#services" class="cta-button secondary">
            <Icon icon="mdi:chevron-down" width="18" height="18" />
            <span>Our Services</span>
          </a>
        </div>
      </div>
    </header>

    <!-- Services -->
    <main id="services" class="main-content">
      <div class="section-header animate-fade-in delay-1">
        <h2 class="section-title text-gradient">What We Offer</h2>
        <p class="section-subtitle">Everything you need in one cozy spot</p>
      </div>

      <div class="services-grid">
        <router-link
          v-for="(service, index) in services"
          :key="service.id"
          :to="service.menuCategory ? `/menu?category=${service.menuCategory}` : '/menu'"
          class="service-card hover-lift animate-fade-in"
          :style="`animation-delay: ${0.1 * (index + 2)}s`"
        >
          <div class="service-icon" :style="`background: ${service.bg}`">
            <Icon :icon="service.icon" width="22" height="22" :style="`color: ${service.iconColor}`" />
          </div>
          <div class="service-text">
            <h3>{{ service.title }}</h3>
            <p>{{ service.desc }}</p>
          </div>
          <Icon icon="mdi:chevron-right" width="16" height="16" class="card-arrow" />
        </router-link>
      </div>
    </main>

    <!-- Barkada Packages Highlight -->
    <section id="packages" class="packages-section">
      <div class="packages-inner">
        <div class="section-header animate-fade-in">
          <h2 class="section-title text-gradient">Barkada Packages</h2>
          <p class="section-subtitle">For groups who deserve more!</p>
        </div>

        <div class="packages-highlight">
          <div
            v-for="(pkg, index) in packages"
            :key="pkg.name"
            class="pkg-card animate-fade-in"
            :class="{ featured: index === 0 }"
            :style="`animation-delay: ${0.1 * (index + 1)}s`"
          >
            <div class="pkg-image">
              <img :src="pkg.image" :alt="pkg.name + ' package'" />
            </div>
            <span v-if="index === 0" class="pkg-popular">Classic</span>
            <h3>{{ pkg.name }}</h3>
            <div class="pkg-price">
              <span class="currency">&#8369;</span>
              <span class="amount">{{ pkg.price }}</span>
              <span class="per">/head</span>
            </div>
            <p class="pkg-group">Group of 4 = <strong>&#8369;{{ pkg.total }}</strong></p>
            <ul>
              <li v-for="item in pkg.inclusions" :key="item">
                <Icon icon="mdi:check" width="14" height="14" />
                {{ item }}
              </li>
            </ul>
          </div>
        </div>

        <div class="packages-cta animate-fade-in">
          <router-link to="/menu?category=packages" class="cta-button primary">
            <span>See Full Details</span>
            <Icon icon="mdi:arrow-right" width="18" height="18" />
          </router-link>
          <div class="cta-contact">
            <Icon icon="mdi:phone" width="16" height="16" />
            <span>Reserve: 0966 179 4944</span>
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
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Hero */
.hero {
  position: relative;
  height: 85vh;
  min-height: 520px;
  max-height: 800px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background-image: url('../assets/bg.jpg');
  background-size: cover;
  background-position: center 30%;
  transform: scale(1.05);
  transition: transform 8s ease-out;
}

.hero:hover .hero-bg {
  transform: scale(1);
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(62, 39, 35, 0.45) 0%,
    rgba(62, 39, 35, 0.65) 40%,
    rgba(62, 39, 35, 0.85) 100%
  );
}

.hero-content {
  position: relative;
  z-index: 1;
  padding: 2rem;
  color: var(--text-light);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.25rem;
}

.hero-title {
  font-size: clamp(2.4rem, 6vw, 4.2rem);
  font-weight: 800;
  line-height: 1.05;
  letter-spacing: -1px;
  text-shadow: 0 4px 24px rgba(0, 0, 0, 0.3);
}

.hero-subtitle {
  font-size: clamp(0.9rem, 1.8vw, 1.15rem);
  max-width: 420px;
  opacity: 0.85;
  line-height: 1.5;
}

.hero-actions {
  display: flex;
  gap: 0.75rem;
  margin-top: 0.5rem;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.8rem 1.5rem;
  font-size: 0.9rem;
  font-weight: 600;
  border: none;
  border-radius: 28px;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.25s cubic-bezier(0.22, 1, 0.36, 1);
}

.cta-button.primary {
  color: white;
  background: var(--accent-color);
  box-shadow: 0 4px 16px rgba(255, 183, 77, 0.35);
}

.cta-button.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(255, 183, 77, 0.45);
  background: #ffc107;
}

.cta-button.secondary {
  color: white;
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.25);
}

.cta-button.secondary:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
}

.cta-button:active {
  transform: translateY(0);
}

/* Main content */
.main-content {
  padding: 4.5rem 1.5rem 5rem;
  max-width: 960px;
  margin: 0 auto;
  flex: 1;
  width: 100%;
  scroll-margin-top: 80px;
}

.section-header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.section-title {
  font-size: clamp(1.8rem, 3.5vw, 2.4rem);
  margin-bottom: 0.4rem;
}

.section-subtitle {
  font-size: 0.95rem;
  color: var(--text-muted);
}

/* Services grid */
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.service-card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.25rem;
  background: var(--bg-card);
  border-radius: var(--radius-lg);
  border: 1px solid rgba(93, 64, 55, 0.05);
  cursor: pointer;
  text-decoration: none;
  color: inherit;
  position: relative;
}

.service-card:hover .card-arrow {
  opacity: 1;
  transform: translateX(2px);
}

.card-arrow {
  position: absolute;
  top: 1.25rem;
  right: 1rem;
  color: var(--text-muted);
  opacity: 0;
  transition: all 0.25s ease;
}

.service-icon {
  width: 44px;
  height: 44px;
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.service-text h3 {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--text-dark);
  margin-bottom: 0.2rem;
}

.service-text p {
  font-size: 0.8rem;
  color: var(--text-muted);
  line-height: 1.45;
}

/* Packages Section */
.packages-section {
  background: linear-gradient(135deg, var(--primary-dark) 0%, #4e342e 100%);
  padding: 4.5rem 1.5rem;
}

.packages-inner {
  max-width: 960px;
  margin: 0 auto;
}

.packages-section .section-title {
  color: white;
  -webkit-text-fill-color: unset;
  background: none;
}

.packages-section .section-subtitle {
  color: rgba(255, 255, 255, 0.6);
}

.packages-highlight {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-bottom: 2.5rem;
}

.pkg-card {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: var(--radius-lg);
  padding: 1.5rem;
  color: white;
  position: relative;
  transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}

.pkg-card:hover {
  background: rgba(255, 255, 255, 0.12);
  transform: translateY(-4px);
}

.pkg-card.featured {
  background: rgba(255, 183, 77, 0.15);
  border-color: rgba(255, 183, 77, 0.3);
}

.pkg-popular {
  position: absolute;
  top: -0.5rem;
  right: 1rem;
  font-size: 0.65rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 0.2rem 0.6rem;
  border-radius: 8px;
  background: var(--accent-color);
  color: var(--primary-dark);
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

.pkg-card h3 {
  font-size: 1.1rem;
  margin-bottom: 0.75rem;
  font-weight: 700;
}

.pkg-card .pkg-price {
  display: flex;
  align-items: baseline;
  gap: 0.1rem;
  margin-bottom: 0.2rem;
}

.pkg-card .currency {
  font-size: 1rem;
  font-weight: 700;
}

.pkg-card .amount {
  font-size: 2rem;
  font-weight: 800;
  line-height: 1;
}

.pkg-card .per {
  font-size: 0.82rem;
  opacity: 0.6;
  margin-left: 0.1rem;
}

.pkg-card .pkg-group {
  font-size: 0.78rem;
  opacity: 0.6;
  margin-bottom: 1rem;
}

.pkg-card .pkg-group strong {
  color: white;
  opacity: 1;
}

.pkg-card ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.pkg-card li {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.8rem;
  opacity: 0.8;
}

.pkg-card li svg {
  color: var(--accent-color);
  flex-shrink: 0;
}

.packages-cta {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
}

.packages-cta .cta-button {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.8rem 1.5rem;
  font-size: 0.9rem;
  font-weight: 600;
  border-radius: 28px;
  text-decoration: none;
  transition: all 0.25s cubic-bezier(0.22, 1, 0.36, 1);
}

.packages-cta .cta-button.primary {
  color: var(--primary-dark);
  background: white;
}

.packages-cta .cta-button.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(255, 255, 255, 0.2);
}

.cta-contact {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.85rem;
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

/* Responsive */
@media (max-width: 768px) {
  .hero {
    height: 70vh;
    min-height: 420px;
  }

  .hero-bg {
    background-position: center 25%;
  }

  .hero-content {
    padding: 1.5rem;
  }

  .hero-actions {
    flex-direction: column;
    width: 100%;
    max-width: 260px;
  }

  .cta-button {
    justify-content: center;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 0.75rem;
  }

  .service-card {
    padding: 1rem;
  }

  .packages-highlight {
    grid-template-columns: 1fr;
  }

  .packages-cta {
    flex-direction: column;
    gap: 1rem;
  }

  .footer-grid {
    flex-direction: column;
    gap: 1.5rem;
  }

  .footer-info {
    flex-direction: column;
    gap: 1.25rem;
  }
}

@media (min-width: 501px) and (max-width: 860px) {
  .services-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .packages-highlight {
    grid-template-columns: 1fr;
  }
}
</style>
