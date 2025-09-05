<template>
  <!-- Geri getirilen HERO alanı -->
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
        <div class="ratio ratio-4x3 rounded-4 overflow-hidden bg-dark">
          <transition name="fade-img" mode="out-in">
            <div class="hero-img" :key="currentImage" :style="{ backgroundImage: `url(${currentImage})` }"></div>
          </transition>
        </div>
      </div>
      <div class="col-md-6">
        <h2 class="h3 playfair">Diyarbakır’ın en taze çiçekleri</h2>
        <p class="text-secondary">Hevsel’den ilhamla tasarlanan buketler, orkideler, çelenkler ve daha fazlası. Her ana yakışan zarafet; şimdi tek dokunuşla kapında.</p>
        <ul class="list-unstyled small text-secondary mb-3">
          <li>• Günlük taze geliş, butik aranjman</li>
          <li>• Aynı gün teslimat, özenli paketleme</li>
          <li>• Özel günlere özel tasarımlar</li>
        </ul>
        <router-link to="/urunler" class="btn btn-dark">Ürünleri Keşfet</router-link>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onBeforeUnmount, computed } from 'vue'

export default defineComponent({
  name: 'HomeView',
  setup() {
    // HERO başlık döngüsü
    const slogans: string[] = [
      "Diyarbakır'ın bir numaralı çiçekçisi",
      "Hevsel'den ilham alan zarif tasarımlar",
      "Her güne taptaze Diyarbakır çiçekleri",
      "Özel günlerinize Sur içi zarafeti"
    ]
    const headlineIndex = ref(0)
    const headline = ref<string>(slogans[0])

    // Tüm ürün görselleri (karışık)
    const allImages = ref<string[]>([
      // Güller
      '/guller/1.webp','/guller/2.webp','/guller/3.webp','/guller/4.webp',
      // Orkideler
      '/orkideler/1.webp','/orkideler/2.webp','/orkideler/3.webp','/orkideler/4.webp','/orkideler/5.webp',
      // Saksı Çiçekleri
      '/saksiCicekleri/1.webp','/saksiCicekleri/2.webp','/saksiCicekleri/3.webp','/saksiCicekleri/4.webp','/saksiCicekleri/5.webp','/saksiCicekleri/6.webp','/saksiCicekleri/7.webp','/saksiCicekleri/8.webp','/saksiCicekleri/9.webp','/saksiCicekleri/10.webp',
      // Açılış Çiçekleri
      '/acilisCicekleri/IMG_4365.webp','/acilisCicekleri/IMG_4366.webp','/acilisCicekleri/IMG_4369.webp','/acilisCicekleri/IMG_4370.webp','/acilisCicekleri/IMG_4371.webp','/acilisCicekleri/IMG_4372.webp',
      // Çelenkler
      '/celenkler/1.webp','/celenkler/2.webp','/celenkler/3.webp','/celenkler/4.webp','/celenkler/5.webp','/celenkler/6.webp','/celenkler/7.webp',
      // Buketler
      '/buketler/1.webp','/buketler/2.webp','/buketler/3.webp','/buketler/4.webp','/buketler/5.webp','/buketler/6.webp',
      // Lüks Buketler
      '/luxBuketler/1.webp','/luxBuketler/2.webp','/luxBuketler/3.webp','/luxBuketler/4.webp','/luxBuketler/5.webp','/luxBuketler/6.webp','/luxBuketler/7.webp','/luxBuketler/8.webp','/luxBuketler/9.webp','/luxBuketler/10.webp','/luxBuketler/11.webp','/luxBuketler/12.webp','/luxBuketler/13.webp','/luxBuketler/14.webp','/luxBuketler/15.webp','/luxBuketler/16.webp','/luxBuketler/17.webp','/luxBuketler/18.webp','/luxBuketler/19.webp',
      // Papatyalar
      '/papatyalar/1.webp','/papatyalar/2.webp','/papatyalar/3.webp',
      // Çikolatalar
      '/Cikolatalar/1.webp','/Cikolatalar/2.webp','/Cikolatalar/3.webp','/Cikolatalar/4.webp','/Cikolatalar/5.webp','/Cikolatalar/6.webp','/Cikolatalar/7.webp','/Cikolatalar/8.webp','/Cikolatalar/9.webp'
    ])

    // Basit karıştırma
    const shuffle = (arr: string[]) => arr
      .map(v => ({ v, r: Math.random() }))
      .sort((a, b) => a.r - b.r)
      .map(o => o.v)

    const imagesShuffled = ref<string[]>(shuffle(allImages.value))
    const idx = ref<number>(0)
    const currentImage = computed(() => imagesShuffled.value[idx.value])

    let timer: number | undefined
    onMounted(() => {
      timer = window.setInterval(() => {
        // Görsel rotasyonu
        idx.value = (idx.value + 1) % imagesShuffled.value.length
        // Hero başlık rotasyonu (her 6sn)
        if ((idx.value % 2) === 0) {
          headlineIndex.value = (headlineIndex.value + 1) % slogans.length
          headline.value = slogans[headlineIndex.value]
        }
      }, 3000)
    })
    onBeforeUnmount(() => { if (timer) window.clearInterval(timer) })
    return { currentImage, headline }
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

.hero-img { position:absolute; inset:0; background: center/cover no-repeat; }
.fade-img-enter-active, .fade-img-leave-active { transition: opacity .6s ease; }
.fade-img-enter-from, .fade-img-leave-to { opacity: 0; }
</style>
