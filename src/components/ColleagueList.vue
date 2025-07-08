<template>
  <div :class="listClasses">
    <!-- Header -->
    <div class="flex items-center justify-between mb-6">
      <h2 class="text-2xl font-semibold text-gray-800">{{ title }}</h2>
      <span v-if="showCount" :class="countBadgeClasses">
        {{ colleagues.length }}
      </span>
    </div>

    <!-- Colleagues List  -->
    <div class="list-container relative min-h-20">
      <transition-group
        name="list"
        tag="div"
        class="space-y-3"
        @before-enter="onBeforeEnter"
        @enter="onEnter"
        @leave="onLeave"
      >
        <div
          v-for="(colleague, index) in colleagues"
          :key="colleague.name"
          :data-index="index"
          class="colleague-item bg-white rounded-xl p-4 shadow-sm border border-gray-200 cursor-pointer transition-all duration-300 hover:shadow-md hover:translate-x-2 hover:scale-105 hover:border-l-4 group"
          :class="colleagueItemClasses"
          @click="handleColleagueClick(colleague)"
        >
          <div class="flex items-center justify-between">
            <div>
              <h3 :class="nameClasses">
                {{ colleague.name }}
              </h3>
              <div class="flex items-center space-x-2 mt-1">
                <span class="text-gray-600 text-sm"
                  >Age: {{ colleague.age }}</span
                >
              </div>
            </div>
            <div :class="arrowClasses">
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  :d="isSelectedList ? 'M15 19l-7-7 7-7' : 'M9 5l7 7-7 7'"
                />
              </svg>
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  name: "ColleagueList",
  props: {
    title: {
      type: String,
      required: true,
    },
    colleagues: {
      type: Array,
      required: true,
    },
    showCount: {
      type: Boolean,
      default: false,
    },
    isSelectedList: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      countChanged: false,
    };
  },
  computed: {
    listClasses() {
      return [
        "rounded-2xl p-6 border-2 transition-all duration-300 hover:shadow-lg hover:-translate-y-1",
        {
          "bg-gray-50 hover:bg-cyan-100 border-gray-200 hover:border-cyan-300":
            !this.isSelectedList,
          "bg-green-50 hover:bg-green-100 border-green-200 hover:border-green-300":
            this.isSelectedList,
        },
      ];
    },
    countBadgeClasses() {
      return [
        "px-3 py-1 rounded-full text-sm font-medium transition-all duration-300",
        {
          "bg-cyan-500 text-white": !this.isSelectedList,
          "bg-green-500 text-white": this.isSelectedList,
          "animate-pulse": this.countChanged,
        },
      ];
    },
    nameClasses() {
      return [
        "font-semibold text-gray-800 text-lg transition-colors duration-300",
        {
          "group-hover:text-cyan-600": !this.isSelectedList,
          "group-hover:text-red-600": this.isSelectedList,
        },
      ];
    },
    arrowClasses() {
      return [
        "opacity-0 group-hover:opacity-100 transition-all duration-300 transform group-hover:translate-x-1",
        {
          "text-cyan-500": !this.isSelectedList,
          "text-red-500": this.isSelectedList,
        },
      ];
    },
    colleagueItemClasses() {
      return {
        "hover:border-l-cyan-500": !this.isSelectedList,
        "hover:border-l-red-500": this.isSelectedList,
        "bg-gradient-to-br from-green-50 to-white": this.isSelectedList,
      };
    },
  },
  watch: {
    colleagues: {
      handler() {
        this.triggerCountAnimation();
      },
      deep: true,
    },
  },
  methods: {
    handleColleagueClick(colleague) {
      this.$emit("select-colleague", colleague);
    },
    triggerCountAnimation() {
      this.countChanged = true;
      setTimeout(() => {
        this.countChanged = false;
      }, 300);
    },
    onBeforeEnter(el) {
      el.style.opacity = "0";
      el.style.transform = "translateY(-20px) scale(0.95)";
    },
    onEnter(el, done) {
      const delay = el.dataset.index * 50;
      setTimeout(() => {
        el.style.transition = "all 0.5s cubic-bezier(0.4, 0, 0.2, 1)";
        el.style.opacity = "1";
        el.style.transform = "translateY(0) scale(1)";
        done();
      }, delay);
    },
    onLeave(el, done) {
      el.style.transition = "all 0.5s cubic-bezier(0.4, 0, 0.2, 1)";
      el.style.opacity = "0";
      el.style.transform = "translateY(20px) scale(0.95)";
      setTimeout(done, 500);
    },
  },
};
</script>

<style scoped>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.list-enter-from {
  opacity: 0;
  transform: translateY(-20px) scale(0.95);
}

.list-leave-to {
  opacity: 0;
  transform: translateY(20px) scale(0.95);
}

.list-leave-active {
  position: absolute;
  width: calc(100% - 1.5rem);
  z-index: 0;
}

.list-move {
  transform: translateZ(0);
}
</style>
