<script setup lang="ts">
interface Author {
  name: string;
  avatar: string;
}

interface ContentItem {
  title: string;
  date: string;
  description: string;
  authors: Author[];
}

interface Props {
  content: ContentItem;
}

defineProps<Props>();
</script>

<template>
  <div class="bg-white/40 backdrop-blur-sm rounded-lg p-6 border border-[#d4c5a8]/30 transition-all duration-500">
    <div class="flex items-start justify-between mb-4">
      <div class="flex-1">
        <h3 class="text-lg font-semibold text-[#3a2f25] mb-1">{{ content.title }}</h3>
        <p class="text-sm text-[#8a7a5f]">{{ content.date }}</p>
      </div>
    </div>

    <p class="text-[#5a4a3a] text-sm leading-relaxed mb-6">
      {{ content.description }}
    </p>

    <div class="space-y-3">
      <p class="text-xs font-semibold text-[#8a7a5f] uppercase tracking-wide">Authors</p>
      <div class="flex flex-wrap gap-4">
        <div
          v-for="(author, index) in content.authors"
          :key="index"
          class="flex items-center gap-2"
        >
          <div class="w-8 h-8 rounded-full bg-[#c4b599] flex items-center justify-center text-white text-sm font-medium">
            {{ author.name.charAt(0) }}
          </div>
          <span class="text-sm text-[#3a2f25]">{{ author.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
