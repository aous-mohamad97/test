<script setup lang="ts">
import { ref } from 'vue';

interface TimelineItem {
  day: string;
  date: string;
}

interface Props {
  items?: TimelineItem[];
}

const props = withDefaults(defineProps<Props>(), {
  items: () => [
    { day: 'DAY 1', date: '16 November' },
    { day: 'DAY 2', date: '17 November' },
    { day: 'DAY 3', date: '18 November' },
    { day: 'DAY 4', date: '19 November' },
    { day: 'DAY 5', date: '20 November' }
  ]
});

const emit = defineEmits<{
  'update:active': [index: number]
}>();

const activeIndex = ref(0);
const hoveredIndex = ref<number | null>(null);

const setActive = (index: number) => {
  activeIndex.value = index;
  emit('update:active', index);
};

const setHovered = (index: number | null) => {
  hoveredIndex.value = index;
};
</script>

<template>
  <div class="relative flex items-center gap-8 px-0 pl-[5vw] md:py-12">
    <div class="flex items-center gap-2 flex-shrink-0">
      <span class="text-sm font-medium text-[#1a1a1a] tracking-wide">Start</span>
      <svg class="flex-shrink-0" width="20" height="12" viewBox="0 0 20 12" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M1 6H19M19 6L14 1M19 6L14 11" stroke="#1a1a1a" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>

    <div class="relative flex-1 flex items-center">
      <div
        class="absolute top-1/2 left-0 right-0 h-px -translate-y-1/2"
        style="background-image: repeating-linear-gradient(to right, #b5a587 0, #b5a587 6px, transparent 6px, transparent 12px)"
      ></div>

      <div class="relative flex justify-between w-full z-10">
        <div
          v-for="(item, index) in props.items"
          :key="index"
          class="flex flex-col items-center gap-5 relative cursor-pointer transition-transform duration-200 hover:-translate-y-0.5"
          @click="setActive(index)"
          @mouseenter="setHovered(index)"
          @mouseleave="setHovered(null)"
        >
          <div
            v-if="index === activeIndex"
            class="absolute -top-3 left-1/2 -translate-x-1/2 w-0 h-0 border-l-[6px] border-l-transparent border-r-[6px] border-r-transparent border-t-[8px] border-t-[#d4894a] animate-fade-in"
          ></div>

          <div
            class="text-center mb-1 transition-all duration-300"
          >
            <div
              class="text-[13px] font-semibold tracking-wider mb-1 transition-colors duration-300"
              :class="{
                'text-[#1a1a1a]': index === activeIndex,
                'text-[#b5a587]': index !== activeIndex && hoveredIndex !== index,
                'text-[#3a3a3a]': hoveredIndex === index && index !== activeIndex
              }"
            >
              {{ item.day }}
            </div>
            <div
              class="text-xs transition-colors duration-300"
              :class="{
                'text-[#1a1a1a] font-medium': index === activeIndex,
                'text-[#c9bda8]': index !== activeIndex && hoveredIndex !== index,
                'text-[#3a3a3a]': hoveredIndex === index && index !== activeIndex
              }"
            >
              {{ item.date }}
            </div>
          </div>

          <div
            class="w-[38px] h-[38px] rounded-full flex items-center justify-center relative transition-all duration-300 shadow-md hover:scale-110 hover:shadow-lg md:w-[38px] md:h-[38px]"
            :class="{
              'bg-[#c4b599] shadow-xl': index === activeIndex,
              'bg-[#e8e3d9]': index !== activeIndex
            }"
          >
            <div
              class="absolute rounded-full border-2 transition-all duration-300 w-7 h-7 md:w-7 md:h-7"
              :class="{
                'border-[#a89678]': index === activeIndex,
                'border-white': index !== activeIndex
              }"
            ></div>
            <div
              class="rounded-full bg-[#8a7a5f] relative z-10 transition-all duration-300"
              :class="{
                'w-3.5 h-3.5 bg-[#6b5d47]': index === activeIndex,
                'w-3 h-3': index !== activeIndex && hoveredIndex !== index,
                'w-3.5 h-3.5': hoveredIndex === index && index !== activeIndex
              }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateX(-50%) translateY(-5px);
  }
  to {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
}

.animate-fade-in {
  animation: fade-in 0.3s ease;
}

@media (max-width: 768px) {
  .text-sm {
    font-size: 12px;
  }

  .gap-5 {
    gap: 0.75rem;
  }

  [class*="text-[13px]"] {
    font-size: 11px;
  }

  [class*="text-xs"] {
    font-size: 10px;
  }
}
</style>
