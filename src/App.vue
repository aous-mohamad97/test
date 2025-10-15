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

const contentDataByDayAndSection: Record<number, Record<number, ContentItem>> = {
  0: {
    0: {
      title: 'Session: The Power of Choice I Opening the Gate',
      date: '16 November',
      description: 'Join us for a transformative exploration of personal agency and the profound impact of our choices. This opening session sets the stage for understanding how individual decisions shape collective narratives and global perspectives. Through interactive discussions and thought-provoking exercises, participants will examine the intersection of personal responsibility and societal change.',
      authors: [
        { name: 'PRECIOUS Mora', avatar: '' },
        { name: 'Lamar Almsaud', avatar: '' }
      ]
    },
    1: {
      title: 'Key Themes: Choice and Agency',
      date: '16 November',
      description: 'The opening day focuses on three interconnected themes: personal agency, collective responsibility, and transformative decision-making. We explore how individual choices ripple through communities and shape societal narratives.',
      authors: [
        { name: 'PRECIOUS Mora', avatar: '' }
      ]
    },
    2: {
      title: 'Session Details: Day 1 Schedule',
      date: '16 November',
      description: 'The session runs from 9:00 AM to 5:00 PM with breaks for networking and reflection. Morning sessions focus on theoretical frameworks, while afternoon activities emphasize practical application through group exercises.',
      authors: [
        { name: 'Lamar Almsaud', avatar: '' }
      ]
    },
    3: {
      title: 'Participant Guide: Preparation for Day 1',
      date: '16 November',
      description: 'To maximize your experience, please come prepared with examples of significant choices you have made. Bring a notebook for reflection exercises. All materials will be provided.',
      authors: [
        { name: 'PRECIOUS Mora', avatar: '' },
        { name: 'Lamar Almsaud', avatar: '' }
      ]
    },
    4: {
      title: 'Resources: Day 1 Reading Materials',
      date: '16 November',
      description: 'Pre-reading materials are available in the participant portal, including articles on decision theory, ethical frameworks, and case studies on transformative choices.',
      authors: [
        { name: 'Lamar Almsaud', avatar: '' }
      ]
    }
  },
  1: {
    0: {
      title: 'Workshop: Global Narratives and Cultural Exchange',
      date: '17 November',
      description: 'Explore diverse cultural perspectives and how they shape our understanding of global events. This workshop brings together voices from different continents to share stories and challenge assumptions about cultural identity and international relations.',
      authors: [
        { name: 'Sofia Chen', avatar: '' },
        { name: 'Marcus Johnson', avatar: '' }
      ]
    },
    1: {
      title: 'Key Themes: Cultural Perspectives',
      date: '17 November',
      description: 'Day 2 explores the intersection of culture, narrative, and global understanding. We examine how different cultural lenses shape interpretations of shared events.',
      authors: [
        { name: 'Sofia Chen', avatar: '' }
      ]
    },
    2: {
      title: 'Session Details: Workshop Structure',
      date: '17 November',
      description: 'The workshop includes breakout sessions with participants from diverse backgrounds, collaborative storytelling exercises, and facilitated discussions on cultural exchange.',
      authors: [
        { name: 'Marcus Johnson', avatar: '' }
      ]
    },
    3: {
      title: 'Participant Guide: Cultural Exchange Protocol',
      date: '17 November',
      description: 'Approach today with curiosity and openness. Be prepared to share aspects of your own cultural background while respectfully engaging with perspectives different from your own.',
      authors: [
        { name: 'Sofia Chen', avatar: '' },
        { name: 'Marcus Johnson', avatar: '' }
      ]
    },
    4: {
      title: 'Resources: Global Narratives Library',
      date: '17 November',
      description: 'Access our curated collection of global narratives, including video interviews, written testimonials, and multimedia presentations from cultures around the world.',
      authors: [
        { name: 'Marcus Johnson', avatar: '' }
      ]
    }
  },
  2: {
    0: {
      title: 'Panel Discussion: Technology and Human Connection',
      date: '18 November',
      description: 'An engaging panel examining the role of technology in modern communication and its impact on human relationships. Industry leaders and academics will discuss the balance between digital innovation and authentic human connection.',
      authors: [
        { name: 'Dr. Aisha Patel', avatar: '' },
        { name: 'James Rodriguez', avatar: '' }
      ]
    },
    1: {
      title: 'Key Themes: Digital Age Dynamics',
      date: '18 November',
      description: 'Today focuses on the paradox of increased connectivity alongside growing isolation. We explore how technology shapes modern relationships and strategies for maintaining authentic connections.',
      authors: [
        { name: 'Dr. Aisha Patel', avatar: '' }
      ]
    },
    2: {
      title: 'Session Details: Panel Format',
      date: '18 November',
      description: 'The panel discussion runs from 10:00 AM to 3:00 PM with Q&A sessions after each segment. Four distinguished panelists will present their perspectives, followed by moderated discussion.',
      authors: [
        { name: 'James Rodriguez', avatar: '' }
      ]
    },
    3: {
      title: 'Participant Guide: Engaging with Panelists',
      date: '18 November',
      description: 'Prepare thoughtful questions about the intersection of technology and human connection. Consider your own experiences with digital communication.',
      authors: [
        { name: 'Dr. Aisha Patel', avatar: '' },
        { name: 'James Rodriguez', avatar: '' }
      ]
    },
    4: {
      title: 'Resources: Technology and Society',
      date: '18 November',
      description: 'Explore research papers, TED talks, and case studies on digital communication, social media psychology, and technology ethics.',
      authors: [
        { name: 'Dr. Aisha Patel', avatar: '' }
      ]
    }
  },
  3: {
    0: {
      title: 'Interactive Session: Building Bridges Across Divides',
      date: '19 November',
      description: 'Participate in collaborative exercises designed to foster understanding and empathy across different perspectives. This session focuses on practical strategies for creating meaningful dialogue in divided communities.',
      authors: [
        { name: 'Emma Thompson', avatar: '' },
        { name: 'Ahmed Hassan', avatar: '' }
      ]
    },
    1: {
      title: 'Key Themes: Unity Through Understanding',
      date: '19 November',
      description: 'Day 4 centers on practical peacebuilding and dialogue facilitation. We explore conflict resolution techniques, empathy development, and strategies for finding common ground.',
      authors: [
        { name: 'Emma Thompson', avatar: '' }
      ]
    },
    2: {
      title: 'Session Details: Interactive Activities',
      date: '19 November',
      description: 'Today features hands-on activities including role-playing exercises, mediation simulations, and collaborative problem-solving challenges.',
      authors: [
        { name: 'Ahmed Hassan', avatar: '' }
      ]
    },
    3: {
      title: 'Participant Guide: Active Participation',
      date: '19 November',
      description: 'Today requires full engagement in interactive exercises. Come prepared to step outside your comfort zone, practice active listening, and engage authentically with diverse viewpoints.',
      authors: [
        { name: 'Emma Thompson', avatar: '' },
        { name: 'Ahmed Hassan', avatar: '' }
      ]
    },
    4: {
      title: 'Resources: Bridge Building Toolkit',
      date: '19 November',
      description: 'Access practical guides on dialogue facilitation, conflict resolution frameworks, and community building strategies. The toolkit includes templates and worksheets.',
      authors: [
        { name: 'Ahmed Hassan', avatar: '' }
      ]
    }
  },
  4: {
    0: {
      title: 'Closing Ceremony: Reflections and Future Pathways',
      date: '20 November',
      description: 'Join us for a reflective conclusion to Gate One, where participants share insights gained throughout the week and chart pathways for continued engagement. This closing session celebrates collective learning and envisions future collaborations.',
      authors: [
        { name: 'Dr. Maria Santos', avatar: '' },
        { name: 'David Kim', avatar: '' }
      ]
    },
    1: {
      title: 'Key Themes: Integration and Continuation',
      date: '20 November',
      description: 'The final day synthesizes the week\'s learnings, helping participants integrate insights and plan for ongoing application. We reflect on personal growth and celebrate collective achievements.',
      authors: [
        { name: 'Dr. Maria Santos', avatar: '' }
      ]
    },
    2: {
      title: 'Session Details: Closing Program',
      date: '20 November',
      description: 'The ceremony runs from 10:00 AM to 2:00 PM, including participant presentations, reflective exercises, and a celebration lunch. Certificates of completion will be awarded.',
      authors: [
        { name: 'David Kim', avatar: '' }
      ]
    },
    3: {
      title: 'Participant Guide: Preparing Your Reflection',
      date: '20 November',
      description: 'Prepare a brief reflection on your week\'s experience, focusing on key insights and intended actions. Consider what you will take forward and how you plan to apply what you have learned.',
      authors: [
        { name: 'Dr. Maria Santos', avatar: '' },
        { name: 'David Kim', avatar: '' }
      ]
    },
    4: {
      title: 'Resources: Continuing the Journey',
      date: '20 November',
      description: 'Access information about alumni networks, ongoing programs, and opportunities for continued learning. Stay connected through our online community platform.',
      authors: [
        { name: 'David Kim', avatar: '' }
      ]
    }
  }
};

const sidebarItems = [
  'Context and Overview',
  'Key Themes',
  'Session Details',
  'Participant Guide',
  'Resources'
];

const activeDay = ref(0);
const activeSection = ref(0);

const currentContent = computed(() => contentDataByDayAndSection[activeDay.value][activeSection.value]);

const computedSidebarItems = computed(() =>
  sidebarItems.map((label, index) => ({
    label,
    active: index === activeSection.value
  }))
);

const handleTimelineClick = (index: number) => {
  activeDay.value = index;
  activeSection.value = 0;
};

const handleSidebarClick = (index: number) => {
  activeSection.value = index;
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
            <Sidebar :items="computedSidebarItems" @item-click="handleSidebarClick" />
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
            <ContentPanel :key="`${activeDay}-${activeSection}`" :content="currentContent" />
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
