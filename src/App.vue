<template>
  <transition name="sweep">
    <div v-if="showSplash" class="splash">
      <div class="splash-inner">
        <div class="splash-mark">
          <img class="splash-logo" src="/logo.png" alt="Rana Flowers logo" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex'" />
          <div class="splash-ring" style="display:none">RF</div>
        </div>
        <div class="splash-brand">
          <div class="splash-title">RANA</div>
          <div class="splash-sub">FLOWERS</div>
          <div class="splash-claim">Diyarbakır'ın bir numaralı çiçekçisi</div>
        </div>
      </div>
    </div>
  </transition>
  <div id="layout">
    <header class="navbar" style="--brand:#222; --primary:#222; --soft:#f6efe9; --accent:#e7f0ec; --muted:#666; --white:#fff;">
      <div class="brand">
        <img class="logo" src="/logo.png" alt="Rana Flowers logo" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex'" />
        <div class="logo-circle" style="display:none">RF</div>
        <div class="brand-text">
          <span class="brand-title">RANA</span>
          <span class="brand-sub">FLOWERS</span>
        </div>
      </div>
      <nav class="menu">
        <router-link to="/">Anasayfa</router-link>
        <router-link to="/urunler">Ürünler</router-link>
        <router-link to="/iletisim">İletişim</router-link>
      </nav>
    </header>

    <main class="content">
      <transition name="view-slide-zoom" mode="out-in">
        <router-view/>
      </transition>
    </main>

    <footer class="footer">
      <p>© {{ new Date().getFullYear() }} Rana Flowers. Tüm hakları saklıdır.</p>
    </footer>
  </div>
  
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue'

export default defineComponent({
  name: 'AppLayout',
  setup() {
    const showSplash = ref(true)
    onMounted(() => {
      setTimeout(() => { showSplash.value = false }, 1800)
    })
    return { showSplash }
  }
})
</script>

<style>
#app { height: 100%; }
/* Splash kapanış animasyonu: yukarı doğru çekilerek dairesel daralma */
.sweep-leave-active { transition: clip-path .7s cubic-bezier(.22,.61,.36,1), transform .7s cubic-bezier(.22,.61,.36,1); }
.sweep-leave-to { clip-path: circle(0% at 50% 0); transform: translateY(-8px); }

.splash {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background:
    radial-gradient(900px 360px at 20% -10%, #f6efe9, transparent),
    radial-gradient(1000px 360px at 100% 0%, #e7f0ec, transparent),
    #fff;
  display: grid;
  place-items: center;
}
.splash-inner {
  display: flex;
  align-items: center;
  gap: 14px;
  transform: translateY(-16px);
  animation: drop .8s ease-out .2s forwards;
}
.splash-mark { display: flex; align-items: center; }
.splash-logo { width: 62px; height: 62px; object-fit: contain; }
.splash-ring {
  width: 58px; height: 58px; border-radius: 50%; border: 2px solid #222;
  display: flex; align-items: center; justify-content: center; font-weight: 800; letter-spacing: 1px;
}
.splash-brand { line-height: 1; text-align: left; }
.splash-title { font-family: 'Playfair Display', 'Cormorant Garamond', serif; font-size: 36px; letter-spacing: 6px; }
.splash-sub { letter-spacing: 6px; font-size: 12px; color: #666; margin-top: 2px; }
.splash-claim { margin-top: 6px; font-style: italic; font-size: 14px; color: #2b2b2b; }
@keyframes drop { to { transform: translateY(0); } }
#layout {
  min-height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr auto;
  background: var(--soft, #faf9f7);
  color: #2b2b2b;
  font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 24px;
  border-bottom: 1px solid #eee;
  background: color-mix(in srgb, var(--white, #fff) 85%, var(--accent, #e7f0ec));
  backdrop-filter: saturate(180%) blur(8px);
  position: sticky;
  top: 0;
  z-index: 10;
  height: 64px;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo { width: 40px; height: 40px; object-fit: contain; }
.logo-circle {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  border: 2px solid var(--brand, #2b2b2b);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  letter-spacing: 1px;
}

.brand-text { line-height: 1; }
.brand-title { font-size: 18px; font-weight: 800; letter-spacing: 2px; }
.brand-sub { font-size: 12px; color: #666; letter-spacing: 3px; display: block; margin-top: 2px; }

.menu { display: flex; gap: 18px; }
.menu a {
  text-decoration: none;
  color: var(--brand, #2b2b2b);
  font-weight: 600;
  padding: 8px 12px;
  border-radius: 8px;
}
.menu a.router-link-exact-active { background: var(--primary, #111); color: #fff; }

.content { padding: 24px; }

/* Router view transition */
.view-slide-zoom-enter-active, .view-slide-zoom-leave-active { transition: transform .38s cubic-bezier(.22,.61,.36,1); }
.view-slide-zoom-enter-from { transform: translateY(18px) scale(.98); }
.view-slide-zoom-leave-to { transform: translateY(-18px) scale(.98); }

/* Prevent layout shift due to scrollbar */
html { scrollbar-gutter: stable both-edges; }

.footer {
  padding: 24px;
  text-align: center;
  color: #666;
  border-top: 1px solid #eee;
  background: #fff;
}
</style>
