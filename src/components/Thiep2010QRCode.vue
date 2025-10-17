<template>
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-br from-pink-100 via-rose-50 to-pink-200 overflow-hidden relative">
    <!-- 🌸 Hoa rơi -->
    <div v-for="n in 20" :key="n" class="absolute animate-flower text-pink-400 text-2xl opacity-80">🌸</div>

    <!-- 💌 Thiệp -->
    <div class="relative perspective z-10">
      <div class="card" :class="{ open: isOpen }" @click="toggleCard">
        <!-- Mặt ngoài thiệp -->
        <div class="front flex flex-col items-center justify-center bg-pink-400 text-white rounded-2xl shadow-2xl p-6 border border-pink-200">
          <div class="text-6xl mb-4 animate-pulse">💌</div>
          <h1 class="text-3xl font-bold">Chúc Mừng 20/10</h1>
          <p class="mt-2 italic text-sm">Nhấn để mở thiệp 🎀</p>
        </div>

        <!-- Mặt trong thiệp -->
        <div class="inside bg-white rounded-2xl shadow-2xl p-8 border border-pink-200 text-center">
          <h2 class="text-3xl font-extrabold text-pink-600 mb-4">💖 Gửi Tới Người Phụ Nữ Tuyệt Vời 💖</h2>
          <p class="text-gray-700 leading-relaxed">
            Cảm ơn bạn vì đã mang đến yêu thương, sự dịu dàng và những nụ cười ngọt ngào cho thế giới này 🌷  
            Chúc bạn luôn xinh đẹp, tự tin và hạnh phúc — không chỉ hôm nay mà là mỗi ngày trong cuộc sống 💕
          </p>
          <p class="mt-6 text-pink-500 font-semibold italic">— 20/10, một ngày thật rực rỡ như chính bạn —</p>

          <div class="mt-8">
            <button @click.stop="toggleCard" class="bg-pink-500 text-white px-4 py-2 rounded-full shadow-md hover:bg-pink-600 transition">
              Đóng thiệp 💫
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- ✨ Ánh sáng lung linh -->
    <div v-for="n in 10" :key="'light'+n" class="absolute w-2 h-2 bg-pink-300 rounded-full animate-twinkle"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isOpen = ref(false);

const toggleCard = () => {
  isOpen.value = !isOpen.value;
};

// hiệu ứng hoa rơi & ánh sáng lung linh
onMounted(() => {
  const flowers = document.querySelectorAll(".animate-flower");
  flowers.forEach((f) => {
    f.style.left = `${Math.random() * 100}%`;
    f.style.animationDelay = `${Math.random() * 5}s`;
    f.style.animationDuration = `${5 + Math.random() * 5}s`;
  });

  const lights = document.querySelectorAll(".animate-twinkle");
  lights.forEach((l) => {
    l.style.top = `${Math.random() * 100}%`;
    l.style.left = `${Math.random() * 100}%`;
    l.style.animationDelay = `${Math.random() * 3}s`;
  });
});
</script>

<style scoped>
/* 🌸 Hoa rơi */
@keyframes flower {
  0% {
    transform: translateY(-10%) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(110vh) rotate(360deg);
    opacity: 0;
  }
}
.animate-flower {
  animation: flower linear infinite;
  position: absolute;
  top: -5%;
  pointer-events: none;
}

/* ✨ Ánh sáng lấp lánh */
@keyframes twinkle {
  0%, 100% {
    opacity: 0.3;
    transform: scale(0.8);
  }
  50% {
    opacity: 1;
    transform: scale(1.4);
  }
}
.animate-twinkle {
  animation: twinkle 2s ease-in-out infinite;
  box-shadow: 0 0 10px 3px #f9c5d1;
}

/* 💌 Hiệu ứng mở thiệp */
.perspective {
  perspective: 1500px;
}
.card {
  width: 320px;
  height: 420px;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 1s ease;
  cursor: pointer;
}
.card.open {
  transform: rotateY(180deg);
}
.front,
.inside {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}
.inside {
  transform: rotateY(180deg);
}

/* ✨ Hiệu ứng mở và xuất hiện */
@keyframes fade-in {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
