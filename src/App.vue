<script setup lang="ts">
import { ref, computed } from 'vue';
import Timeline from './components/Timeline.vue';
import ContentPanel from './components/ContentPanel.vue';
import Sidebar from './components/Sidebar.vue';

interface TimelineItem {
  day: string;
  date: string;
}

interface ContentItem {
  title: string;
  date: string;
  description: string;
  authors: Array<{ name: string; avatar: string }>;
}

const timelineItems: TimelineItem[] = [
  { day: 'DAY 1', date: '16 November' },
  { day: 'DAY 2', date: '17 November' },
  { day: 'DAY 3', date: '18 November' },
  { day: 'DAY 4', date: '19 November' },
  { day: 'DAY 5', date: '20 November' }
];

const contentData: ContentItem[] = [
  {
    title: 'Session: The Power of Choice I Opening the Gate',
    date: '16 November',
    description: 'Join us for a transformative exploration of personal agency and the profound impact of our choices. This opening session sets the stage for understanding how individual decisions shape collective narratives and global perspectives. Through interactive discussions and thought-provoking exercises, participants will examine the intersection of personal responsibility and societal change.',
    authors: [
      { name: 'PRECIOUS Mora', avatar: '' },
      { name: 'Lamar Almsaud', avatar: '' }
    ]
  },
  {
    title: 'Workshop: Global Narratives and Cultural Exchange',
    date: '17 November',
    description: 'Explore diverse cultural perspectives and how they shape our understanding of global events. This workshop brings together voices from different continents to share stories and challenge assumptions about cultural identity and international relations.',
    authors: [
      { name: 'Sofia Chen', avatar: '' },
      { name: 'Marcus Johnson', avatar: '' }
    ]
  },
  {
    title: 'Panel Discussion: Technology and Human Connection',
    date: '18 November',
    description: 'An engaging panel examining the role of technology in modern communication and its impact on human relationships. Industry leaders and academics will discuss the balance between digital innovation and authentic human connection.',
    authors: [
      { name: 'Dr. Aisha Patel', avatar: '' },
      { name: 'James Rodriguez', avatar: '' }
    ]
  },
  {
    title: 'Interactive Session: Building Bridges Across Divides',
    date: '19 November',
    description: 'Participate in collaborative exercises designed to foster understanding and empathy across different perspectives. This session focuses on practical strategies for creating meaningful dialogue in divided communities.',
    authors: [
      { name: 'Emma Thompson', avatar: '' },
      { name: 'Ahmed Hassan', avatar: '' }
    ]
  },
  {
    title: 'Closing Ceremony: Reflections and Future Pathways',
    date: '20 November',
    description: 'Join us for a reflective conclusion to Gate One, where participants share insights gained throughout the week and chart pathways for continued engagement. This closing session celebrates collective learning and envisions future collaborations.',
    authors: [
      { name: 'Dr. Maria Santos', avatar: '' },
      { name: 'David Kim', avatar: '' }
    ]
  }
];

const sidebarItems = [
  'Context and Overview',
  'Key Themes',
  'Session Details',
  'Participant Guide',
  'Resources'
];

const activeDay = ref(0);

const currentContent = computed(() => contentData[activeDay.value]);

const computedSidebarItems = computed(() =>
  sidebarItems.map((label, index) => ({
    label,
    active: index === 0
  }))
);

const handleTimelineClick = (index: number) => {
  activeDay.value = index;
};
</script>

<template>
  <div class="min-h-screen bg-[#f5f2ec]">
    <div class="w-full max-w-7xl mx-auto px-4 md:px-8 py-8 md:py-12">
      <div class="text-center mb-12 md:mb-16">
        <h1 class="text-3xl md:text-5xl font-serif text-[#5a4a3a] mb-3 md:mb-4">Gate One:</h1>
        <p class="text-base md:text-lg text-[#8a7a5f]">Opening Narratives & Global Perspectives</p>
      </div>

      <div class="mb-12 md:mb-16">
        <Timeline :items="timelineItems" @update:active="handleTimelineClick" />
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 md:gap-8">
        <div class="lg:col-span-3 order-2 lg:order-1">
          <div class="bg-white/30 backdrop-blur-sm rounded-lg p-4 md:p-6 border border-[#d4c5a8]/20 sticky top-8">
            <h3 class="text-sm font-semibold text-[#3a2f25] mb-4 uppercase tracking-wide">Navigation</h3>
            <Sidebar :items="computedSidebarItems" />
          </div>
        </div>

        <div class="lg:col-span-9 order-1 lg:order-2">
          <transition
            enter-active-class="transition-all duration-500 ease-out"
            leave-active-class="transition-all duration-300 ease-in"
            enter-from-class="opacity-0 translate-y-4"
            enter-to-class="opacity-100 translate-y-0"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 -translate-y-4"
            mode="out-in"
          >
            <ContentPanel :key="activeDay" :content="currentContent" />
          </transition>
        </div>
      </div>
    </div>

    <div class="fixed bottom-0 left-0 right-0 h-32 pointer-events-none"
         style="background: linear-gradient(to top, rgba(245, 242, 236, 0.8) 0%, transparent 100%);">
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lora:wght@400;600&display=swap');

h1 {
  font-family: 'Lora', serif;
}
</style>
