<template>
  <section class="hero container py-5">
    <div class="row align-items-center justify-content-center text-center">
      <div class="col-lg-10">
        <div class="brand-badge letter-space-2 mb-2">RANA FLOWERS</div>
        <h1 class="display-4 fw-bold italic fade-slide playfair fancy-title">
          <transition name="headline-swipe" mode="out-in">
            <span :key="headline">{{ headline }}</span>
          </transition>
        </h1>
        <p class="subtitle playfair">Hevsel'in ruhunu taşıyan zarif aranjmanlar</p>
        <p class="text-secondary mx-auto" style="max-width: 680px;">Diyarbakır'ın tarihi dokusundan ilham alan butik tasarımlar ve taptaze buketlerle özel anlarınıza eşlik ediyoruz.</p>
        <div class="d-flex gap-2 justify-content-center mt-3">
          <router-link to="/urunler" class="btn btn-dark px-4">Ürünleri Gör</router-link>
          <router-link to="/iletisim" class="btn btn-outline-dark px-4">İletişime Geç</router-link>
        </div>
      </div>
    </div>
  </section>

  <section class="container pb-4">
    <div class="row g-3">
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <div class="card-body text-center">
            <h3 class="h5">Taze & Günlük</h3>
            <p class="text-secondary mb-0">Her gün taze gelen çiçeklerle hazırlanan özenli aranjmanlar.</p>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <div class="card-body text-center">
            <h3 class="h5">Butik Tasarım</h3>
            <p class="text-secondary mb-0">Her zevke uygun minimal ve şık tasarımlar.</p>
          </div>
        </div>
      </div>
      <div class="col-md-4">
        <div class="card h-100 shadow-sm">
          <div class="card-body text-center">
            <h3 class="h5">Hızlı Teslimat</h3>
            <p class="text-secondary mb-0">Şehir içi aynı gün teslimat seçenekleri.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="container py-4">
    <div class="row align-items-center g-3">
      <div class="col-md-6">
        <div class="ratio ratio-4x3 rounded-4 border bg-light" style="background:url('https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1200&auto=format&fit=crop') center/cover no-repeat;"></div>
      </div>
      <div class="col-md-6">
        <h2 class="h3">Her duyguya Diyarbakır zarafeti</h2>
        <p class="text-secondary">Sur içinin zarif çizgileri ve Hevsel'in renklerinden esinlenen koleksiyonumuzla sevginizi en şık şekilde ifade edin.</p>
        <router-link to="/urunler" class="btn btn-dark">Koleksiyonu Keşfet</router-link>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onBeforeUnmount } from 'vue'

export default defineComponent({
  name: 'HomeView',
  setup() {
    const slogans: string[] = [
      "Diyarbakır'ın bir numaralı çiçekçisi",
      "Hevsel'den ilham alan zarif tasarımlar",
      "Her güne taptaze Diyarbakır çiçekleri",
      "Özel günlerinize Sur içi zarafeti"
    ]
    const index = ref(0)
    const headline = ref<string>(slogans[0])
    let timer: number | undefined
    onMounted(() => {
      timer = window.setInterval(() => {
        index.value = (index.value + 1) % slogans.length
        headline.value = slogans[index.value]
      }, 6000)
    })
    onBeforeUnmount(() => { if (timer) window.clearInterval(timer) })
    return { headline }
  }
})
</script>

<style scoped>
.playfair { font-family: 'Playfair Display', 'Cormorant Garamond', serif; }
.letter-space-2 { letter-spacing: 2px; }


.italic { font-style: italic; }
.fade-slide {
  opacity: 0;
  transform: translateY(-18px);
  animation: fadeSlideIn .9s ease-out .2s forwards;
}
@keyframes fadeSlideIn {
  to { opacity: 1; transform: translateY(0); }
}

.brand-badge {
  display: inline-block;
  padding: 6px 14px;
  border-radius: 999px;
  border: 1px solid rgba(0,0,0,.2);
  background: #e7f0ec;
  color: #1f1f1f;
  font-weight: 600;
}

.fancy-title {
  position: relative;
  line-height: 1.15;
  background: linear-gradient(90deg, #1f1f1f, #4b4b4b);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.fancy-title::before, .fancy-title::after {
  content: "";
  position: absolute;
  top: 50%;
  width: 14%;
  height: 1px;
  background: linear-gradient(90deg, transparent, #999, transparent);
}
.fancy-title::before { left: -2%; }
.fancy-title::after { right: -2%; }

.subtitle { margin-top: 6px; font-style: italic; color: #6c757d; }

/* Headline rotating transition (no opacity) */
.headline-swipe-enter-active, .headline-swipe-leave-active {
  transition: transform .5s cubic-bezier(.22,.61,.36,1), clip-path .5s cubic-bezier(.22,.61,.36,1);
  will-change: transform, clip-path;
  display: inline-block;
}
.headline-swipe-enter-from {
  transform: translateY(14px) scale(.98) skewY(2deg);
  clip-path: polygon(0 0, 0 0, 0 100%, 0 100%);
}
.headline-swipe-leave-to {
  transform: translateY(-14px) scale(.98) skewY(-2deg);
  clip-path: polygon(100% 0, 100% 0, 100% 100%, 100% 100%);
}
</style>
