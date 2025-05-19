<template>
  <header
    class="flex justify-between items-center p-6 bg-opacity-50 relative z-20"
  >
    <div class="font-lao text-3xl font-bold">
      <div class="flex space-x-1">
        <ChangeLanguage />
      </div>
    </div>
    <!-- Mobile Toggle Button -->
    <div class="md:hidden z-30">
      <button
        type="button"
        class="block focus:outline-none"
        @click="isMenuOpen = !isMenuOpen"
      >
        <span v-if="isMenuOpen" class="text-5xl">
          <img
            src="https://img.icons8.com/ios-filled/100/ffffff/delete-sign.png"
            alt="close"
            width="50"
            height="50"
          />
        </span>
        <span v-else class="text-5xl">
          <img
            src="https://img.icons8.com/ios-filled/100/ffffff/menu--v6.png"
            alt="menu"
            width="50"
            height="50"
          />
        </span>
      </button>
    </div>
    <!-- Navbar Link -->
    <nav
      :class="[
        'fixed inset-0 z-20 flex flex-col items-center justify-center bg-[#111827] md:relative md:bg-transparent md:flex md:justify-between md:flex-row',
        isMenuOpen ? 'block' : 'hidden',
      ]"
    >
      <ul
        class="flex flex-col items-center space-y-5 md:flex-row md:space-x-5 md:space-y-0"
      >
        <li
          v-for="item in check === 'en'
            ? Menu_en
            : check === 'vn'
            ? Menu_vn
            : Menu"
          :key="item.name"
        >
          <a
            :href="item.href"
            class="font-lao block text-white transition hover:text-primary ease-linear text-2xl md:text-lg"
            @click="scrollToSection(item.href)"
          >
            {{ item.name }}
          </a>
        </li>
      </ul>
    </nav>
  </header>
</template>
<script setup>
import { ref, watch } from "vue";
import { useI18n } from "vue-i18n";
import { currentLanguage } from "../i18n";
import ChangeLanguage from "./ChangeLanguage.vue";
const Menu = ref([
  // { name: "Services", href: "#services" },
  { name: "ກ່ຽວກັບຂ້ອຍ", href: "#about" },
  { name: "ທັກສະ", href: "#skills" },
  // { name: "Projects", href: "#projects" },
  // { name: "Testimonials", href: "#testimonials" },
  { name: "ຊ່ອງທາງຕິດຕໍ່", href: "#contact" },
]);
const Menu_en = ref([
  // { name: "Services", href: "#services" },
  { name: "About Me", href: "#about" },
  { name: "Skills", href: "#skills" },
  // { name: "Projects", href: "#projects" },
  // { name: "Testimonials", href: "#testimonials" },
  { name: "Contact", href: "#contact" },
]);
const Menu_vn = ref([
  // { name: "Services", href: "#services" },
  { name: "Giới thiệu", href: "#about" },
  { name: "Kỹ năng", href: "#skills" },
  // { name: "Projects", href: "#projects" },
  // { name: "Testimonials", href: "#testimonials" },
  { name: "Liên hệ", href: "#contact" },
]);
const isMenuOpen = ref(false);
const scrollToSection = (href) => {
  isMenuOpen.value = false;
  const section = document.querySelector(href);
  if (section) {
    section.scrollIntoView({ behavior: "smooth" });
  }
};
// Handle language switching
const { locale } = useI18n();
const check = ref(currentLanguage.value);
// Watch for changes in the global language state and update the i18n locale
watch(currentLanguage, (newLanguage) => {
  locale.value = newLanguage;
  check.value = newLanguage;
});

</script>
