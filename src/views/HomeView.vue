<template>
  <NavbarFilter @changeFilter="handleFilter" :current="current" />
  <div v-if="projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="handleDelete"
        @complete="handleComplete"
      />
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import NavbarFilter from "../components/NavbarFilter.vue";
import AddProject from "./AddProject.vue";
export default {
  name: "HomeView",
  components: { SingleProject, AddProject, NavbarFilter },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((element) => element.id !== id);
    },
    handleComplete(id) {
      let p = this.projects.find((item) => item.id === id);
      p.complete = !p.complete;
    },
    handleFilter(by) {
      this.current = by;
    },
    
  },
  computed: {
      filteredProjects() {
        if (this.current === "completed") {
          return this.projects.filter((item) => item.complete);
        } else if (this.current === "ongoing") {
          return this.projects.filter((item) => !item.complete);
        } else if (this.current === "all") {
          return this.projects;
        }
      },
    },
};
</script>
