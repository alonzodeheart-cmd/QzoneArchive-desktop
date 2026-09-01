<script setup lang="ts">
import { ref } from "vue";
import qrImage from "../assets/promo/qr.png";
import posterImage from "../assets/promo/poster.jpg";

// 首页顶部推广横幅（衍生分发版新增）。仅出现在概览首页，可关闭，点击查看完整海报。
const visible = ref(true);
const showPoster = ref(false);
</script>

<template>
  <section v-if="visible" class="promo-banner" aria-label="推广">
    <button class="promo-close" type="button" aria-label="关闭推广" @click="visible = false">
      <i class="pi pi-times" />
    </button>
    <div class="promo-body">
      <div class="promo-text">
        <h4>碎片时间赚点零花<span class="promo-tag">推广</span></h4>
        <p>简单小任务，1 元起提，每天几十分钟就有收获</p>
        <button class="promo-btn" type="button" @click="showPoster = true">
          <i class="pi pi-qrcode" /><span>扫码看看</span>
        </button>
      </div>
      <img class="promo-qr" :src="qrImage" alt="推广二维码" title="点击查看大图" @click="showPoster = true" />
    </div>

    <div v-if="showPoster" class="promo-modal" @click.self="showPoster = false">
      <div class="promo-modal-box">
        <button class="promo-modal-close" type="button" aria-label="关闭" @click="showPoster = false">
          <i class="pi pi-times" />
        </button>
        <img :src="posterImage" alt="推广海报" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.promo-banner {
  position: relative;
  margin-top: 20px;
  padding: 18px 22px;
  border: 1px solid #ffd9b8;
  border-radius: 18px;
  background: linear-gradient(120deg, #fff7ef, #fffdf8);
  box-shadow: 0 12px 32px rgba(230, 130, 30, .08);
}
.promo-body {
  display: flex;
  align-items: center;
  gap: 20px;
}
.promo-text {
  min-width: 0;
  flex: 1;
}
.promo-text h4 {
  display: flex;
  align-items: center;
  gap: 9px;
  margin: 0;
  color: #7a3a00;
  font-size: 16px;
}
.promo-tag {
  padding: 1px 7px;
  border: 1px solid #ffd9b8;
  border-radius: 5px;
  color: #a06a33;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: .08em;
}
.promo-text p {
  margin: 6px 0 12px;
  color: #b07a44;
  font-size: 13px;
}
.promo-btn {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 8px 18px;
  color: #fff;
  border: 0;
  border-radius: 999px;
  background: linear-gradient(135deg, #ff6a00, #ffa800);
  box-shadow: 0 6px 16px rgba(255, 122, 0, .28);
  cursor: pointer;
  font-size: 13px;
  font-weight: 600;
  transition: transform .15s, box-shadow .15s;
}
.promo-btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 9px 20px rgba(255, 122, 0, .36);
}
.promo-qr {
  width: 86px;
  height: 86px;
  flex: 0 0 86px;
  padding: 5px;
  border: 1px solid #ffe2c4;
  border-radius: 13px;
  background: #fff;
  object-fit: contain;
  cursor: zoom-in;
}
.promo-close {
  position: absolute;
  top: 10px;
  right: 12px;
  display: grid;
  width: 26px;
  height: 26px;
  place-items: center;
  color: #c08a5a;
  border: 0;
  border-radius: 50%;
  background: transparent;
  cursor: pointer;
}
.promo-close:hover {
  background: #ffedd9;
}
.promo-modal {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 28px;
  background: rgba(20, 24, 28, .62);
}
.promo-modal-box {
  position: relative;
  width: min(92vw, 380px);
  padding: 14px;
  border-radius: 18px;
  background: #fff;
}
.promo-modal-box img {
  display: block;
  width: 100%;
  border-radius: 12px;
}
.promo-modal-close {
  position: absolute;
  top: 8px;
  right: 8px;
  display: grid;
  width: 30px;
  height: 30px;
  place-items: center;
  color: #555;
  border: 0;
  border-radius: 50%;
  background: rgba(255, 255, 255, .9);
  cursor: pointer;
}

/* 暗色主题适配 */
.app-dark .promo-banner {
  border-color: #5a4022;
  background: linear-gradient(120deg, #2a2118, #221d17);
  box-shadow: 0 12px 32px rgba(0, 0, 0, .25);
}
.app-dark .promo-text h4 { color: #ffcf9e; }
.app-dark .promo-tag { border-color: #6b4c28; color: #d6a877; }
.app-dark .promo-text p { color: #c79b6c; }
.app-dark .promo-qr,
.app-dark .promo-modal-box,
.app-dark .promo-modal-close { background: #fff; }

@media (max-width: 767px) {
  .promo-banner { padding: 16px; border-radius: 16px; }
  .promo-qr { width: 70px; height: 70px; flex-basis: 70px; }
  .promo-text h4 { font-size: 15px; }
}
</style>
