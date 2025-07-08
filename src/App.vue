<template>
  <div
    class="min-h-screen bg-gradient-to-br from-cyan-500 via-teal-500 to-emerald-500 p-4 sm:p-6 lg:p-8"
  >
    <div class="max-w-7xl mx-auto">
      <div class="bg-white rounded-3xl shadow-2xl overflow-hidden">
        <!-- Header -->
        <div
          class="bg-gradient-to-br from-cyan-500 to-teal-400 text-white p-8 text-center"
        >
          <h1 class="text-4xl font-light mb-3">Colleagues Selector</h1>
          <p class="text-cyan-100 opacity-90">
            Click on colleagues to move them between lists
          </p>
        </div>

        <div class="p-8">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
            <!-- Available Colleagues -->
            <ColleagueList
              title="Available Colleagues"
              :colleagues="availableColleagues"
              :show-count="true"
              :is-selected-list="false"
              @select-colleague="moveToSelected"
            />

            <!-- Selected Colleagues -->
            <ColleagueList
              title="Selected Colleagues"
              :colleagues="selectedColleagues"
              :show-count="true"
              :is-selected-list="true"
              @select-colleague="moveToAvailable"
            />
          </div>

          <!-- Overview -->
          <div
            class="text-center p-4 bg-gradient-to-r from-cyan-50 to-green-50 rounded-2xl border border-gray-200"
          >
            <p class="text-gray-600">
              <span class="font-semibold text-cyan-600">{{
                availableColleagues.length
              }}</span>
              available,
              <span class="font-semibold text-green-600">{{
                selectedColleagues.length
              }}</span>
              selected
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ColleagueList from "./components/ColleagueList.vue";

export default {
  name: "App",
  components: {
    ColleagueList,
  },
  data() {
    return {
      originalColleagues: [
        { name: "Joseph", age: 26 },
        { name: "Daniel", age: 38 },
        { name: "Joshua", age: 50 },
        { name: "Yuri", age: 42 },
        { name: "Rose", age: 25 },
        { name: "Maria", age: 29 },
        { name: "Mark", age: 40 },
        { name: "Pauline", age: 38 },
        { name: "Jasmine", age: 38 },
        { name: "Angel", age: 39 },
      ],
      selectedColleagues: [],
    };
  },
  computed: {
    availableColleagues() {
      return this.originalColleagues.filter(
        (colleague) =>
          !this.selectedColleagues.some(
            (selected) => selected.name === colleague.name
          )
      );
    },
  },
  methods: {
    moveToSelected(colleague) {
      if (
        !this.selectedColleagues.some(
          (selected) => selected.name === colleague.name
        )
      ) {
        this.selectedColleagues.push(colleague);
      }
    },
    moveToAvailable(colleague) {
      this.selectedColleagues = this.selectedColleagues.filter(
        (selected) => selected.name !== colleague.name
      );
    },
  },
};
</script>
