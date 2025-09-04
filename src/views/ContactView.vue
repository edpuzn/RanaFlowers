<template>
  <section class="contact container py-3">
    <div class="row g-3 align-items-stretch">
      <div class="col-lg-6">
        <div class="info-card h-100">
          <div class="brand-badge mb-2 text-center">RANA FLOWERS</div>
          <h2 class="h3 playfair mb-2 text-center">Diyarbakır'ın Zarafeti</h2>
          <p class="text-secondary small text-center mb-3">Diyarbakır Kayapınar'da, şehrin ruhunu çiçeklerle buluşturuyoruz.</p>
          <ul class="list-unstyled info-list">
            <li><i class="bi bi-geo-alt"></i> Fırat, Fırat Blv. No:43 A, 21090 Kayapınar/Diyarbakır</li>
            <li><i class="bi bi-telephone"></i> <a class="link-dark" href="tel:+905536026121">0553 602 61 21</a></li>
          </ul>

          <div class="d-flex gap-2 justify-content-center mt-2">
            <a class="btn btn-dark" target="_blank" rel="noopener" href="https://www.google.com/maps/place/Rana+Flowers/@37.9332758,40.1669807,17z/data=!3m1!4b1!4m6!3m5!1s0x40751f9e5e9132d3:0x42ac0fb6e74ff4d1!8m2!3d37.9332758!4d40.1695556!16s%2Fg%2F11mdnjmw66?entry=ttu"><i class="bi bi-sign-turn-right"></i> Yol Tarifi</a>
            <a class="btn btn-outline-dark" href="tel:+905536026121"><i class="bi bi-telephone-outbound"></i> Ara</a>
          </div>

          <div class="mt-3">
            <button class="btn btn-link p-0" data-bs-toggle="collapse" data-bs-target="#hours" aria-expanded="false" aria-controls="hours">
              <i class="bi bi-clock"></i> Çalışma Saatleri
            </button>
            <div id="hours" class="collapse">
              <ul class="small text-secondary mb-0">
                <li>Her gün: 09:00 – 21:00</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="col-lg-6">
        <div class="map-card h-100">
          <iframe class="map-frame" title="Rana Flowers Harita" loading="lazy" allowfullscreen referrerpolicy="no-referrer-when-downgrade"
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3167.537622829015!2d40.1669807!3d37.9332758!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x40751f9e5e9132d3%3A0x42ac0fb6e74ff4d1!2sRana%20Flowers!5e0!3m2!1str!2str!4v1730380000000!5m2!1str!2str"></iframe>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({ name: 'ContactView' })
</script>

<style scoped>
.playfair { font-family: 'Playfair Display', 'Cormorant Garamond', serif; }
.contact .brand-badge { display:inline-block; padding:6px 14px; border-radius:999px; border:1px solid rgba(0,0,0,.15); background:#e7f0ec; letter-spacing:2px; font-weight:600; }
.info-line { display:grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap:8px; background:#fff; border:1px solid #eee; border-radius:14px; padding:12px; }
.info-line .label { font-weight:700; margin-right:6px; }

.map-full { width: 100%; }
.map-frame { width: 100%; height: 60vh; min-height: 420px; border: 0; display: block; }
</style>


