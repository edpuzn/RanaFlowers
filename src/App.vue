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
    <div class="topbar">
      <div class="topbar-inner">
        <a class="tb-phone" href="tel:+905536026121"><i class="bi bi-telephone"></i> 0553 602 61 21</a>
        <div class="tb-social">
          <a href="https://wa.me/905536026121" target="_blank" rel="noopener" aria-label="WhatsApp"><i class="bi bi-whatsapp"></i></a>
          <a href="https://instagram.com/ranaflowers21" target="_blank" rel="noopener" aria-label="Instagram"><i class="bi bi-instagram"></i></a>
        </div>
      </div>
    </div>
    <header class="navbar" style="--brand:#222; --primary:#222; --soft:#f6efe9; --accent:#e7f0ec; --muted:#666; --white:#fff;">
      <div class="navbar-inner">
        <div class="brand">
          <div class="logo-circle">RF</div>
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
      </div>
    </header>

    <main class="content">
      <transition name="view-slide-zoom" mode="out-in">
        <router-view/>
      </transition>
    </main>

    <footer class="footer">
      <div class="footer-wrap">
        <div class="footer-col">
          <div class="footer-title"><i class="bi bi-headset"></i> Çağrı Merkezi</div>
          <a class="footer-phone" href="tel:+905536026121">0553 602 61 21</a>
          <div class="footer-item">
            <i class="bi bi-geo-alt"></i>
            <span>Fırat Mah. Fırat Blv. No:43 A, Kayapınar / Diyarbakır</span>
          </div>
          <div class="footer-social">
            <a class="whatsapp" href="https://wa.me/905536026121" target="_blank" rel="noopener" aria-label="WhatsApp"><i class="bi bi-whatsapp"></i></a>
            <a class="instagram" href="https://instagram.com/ranaflowers21" target="_blank" rel="noopener" aria-label="Instagram"><i class="bi bi-instagram"></i></a>
          </div>
        </div>

        <div class="footer-col">
          <div class="footer-title"><i class="bi bi-list-ul"></i> Kategoriler</div>
          <ul class="footer-cats">
            <li><router-link :to="{ path: '/urunler', query: { cat: 'lux' } }">Lüks Buketler</router-link></li>
            <li><router-link :to="{ path: '/urunler', query: { cat: 'papatyalar' } }">Papatyalar</router-link></li>
            <li><router-link :to="{ path: '/urunler', query: { cat: 'cikolatalar' } }">Çikolatalar</router-link></li>
            <li class="more"><router-link to="/urunler">Daha fazlasını görüntüle</router-link></li>
          </ul>
        </div>

        <div class="footer-col">
          <div class="footer-title"><i class="bi bi-info-circle"></i> Bilgilendirme</div>
          <ul>
            <li><router-link to="/iletisim">İletişim</router-link></li>
            <li><a href="#">Hakkımızda</a></li>
            <li><a href="#">Kullanım Koşulları</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <div class="footer-title"><i class="bi bi-credit-card"></i> Ödeme</div>
          <div class="cards">
            <span class="pay" aria-label="VISA logo">
              <img src="/brands/visa.svg" alt="Visa" />
            </span>
            <span class="pay" aria-label="Mastercard logo">
              <img src="/brands/mastercard.svg" alt="Mastercard" />
            </span>
            <span class="pay" aria-label="TROY logo">
              <img src="/brands/troy.png" alt="Troy" />
            </span>
          </div>
        </div>
      </div>
      <div class="footer-bottom">© {{ new Date().getFullYear() }} Rana Flowers • Diyarbakır</div>
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

.topbar {
  background: #111;
  color: #fff;
  font-size: 12px;
}
.topbar-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 6px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.tb-phone { color:#fff; text-decoration:none; display:flex; align-items:center; gap:6px; font-weight:700; }
.tb-social { display:flex; gap:10px; }
.tb-social a { color:#fff; opacity:.85; }
.tb-social a:hover { opacity:1; }

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

.navbar-inner { max-width: 1200px; margin: 0 auto; width: 100%; display:flex; align-items:center; justify-content:space-between; }

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

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
  background: radial-gradient(80% 80% at 30% 20%, #ffffff, #f6efe9);
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
  padding: 32px 24px 16px;
  color: #333;
  border-top: 1px solid #eee;
  background: linear-gradient(180deg, #ffffff, #f7f6f4);
}

.footer-wrap {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
  align-items: start;
}
.footer-col { background:#fff; border:1px solid #eee; border-radius:14px; padding:14px; }
.footer-title { font-weight:800; display:flex; align-items:center; gap:8px; margin-bottom:8px; }
.footer-phone { display:inline-block; font-weight:800; font-size:20px; color:#111; text-decoration:none; }
.footer-item { display:flex; gap:8px; color:#555; margin-top:8px; }
.footer-social { display:flex; gap:16px; margin-top:10px; justify-content:center; }
.footer-social a { color:#111; font-size:22px; line-height:1; }
.footer-social a:hover { transform: translateY(-1px); }
.footer-col ul { list-style:none; padding-left:0; margin:0; }
.footer-col li { margin:6px 0; }
.footer-col a { text-decoration:none; color:#333; }
.footer-cats { font-size: 14px; }
.footer-cats .more { margin-top:8px; font-weight:700; }
.cards { display:flex; flex-wrap:wrap; gap:8px; }
.pay { width:110px; height:48px; border:1px solid #ddd; border-radius:10px; display:flex; align-items:center; justify-content:center; background:#fff; }
.pay img { max-width:88px; max-height:28px; }
.footer-bottom { text-align:center; color:#666; margin-top:12px; font-size:12px; }
</style>
