<script setup lang="ts">
interface SidebarItem {
  label: string;
  active: boolean;
}

interface Props {
  items: SidebarItem[];
}

defineProps<Props>();

const emit = defineEmits<{
  'item-click': [index: number]
}>();

const handleItemClick = (index: number) => {
  emit('item-click', index);
};
</script>

<template>
  <div class="space-y-2">
    <div
      v-for="(item, index) in items"
      :key="index"
      class="flex items-center gap-3 py-3 px-4 rounded-lg transition-all duration-300 cursor-pointer"
      :class="item.active ? 'bg-white/50 border border-[#d4c5a8]/40' : 'hover:bg-white/20'"
      @click="handleItemClick(index)"
    >
      <div
        class="w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0 transition-all duration-300"
        :class="item.active ? 'bg-[#c4b599]' : 'bg-[#e8e3d9]'"
      >
        <div
          class="w-3 h-3 rounded-full transition-all duration-300"
          :class="item.active ? 'bg-[#8a7a5f]' : 'bg-[#b5a587]'"
        ></div>
      </div>
      <span
        class="text-sm transition-colors duration-300"
        :class="item.active ? 'text-[#3a2f25] font-medium' : 'text-[#8a7a5f]'"
      >
        {{ item.label }}
      </span>
    </div>
  </div>
</template>
