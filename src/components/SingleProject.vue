<template>
  <div class="projects" :class="{ done: project.complete }">
    <div class="actions">
      <h3 @click="handleTitle">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons">edit</span>
        </router-link>
        <span class="material-icons" @click="changeComplete">done</span>
        <span class="material-icons" @click="handleDelete">delete</span>
      </div>
    </div>
    <div class="details">
      <p v-if="showDetail">{{ project.detail }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showDetail: false,
      url: "http://localhost:3000/projects/" + this.project.id,
      
    };
  },
  props: ["project"],
  methods: {
    handleTitle() {
      this.showDetail = !this.showDetail;
    },
    handleDelete() {
      fetch(this.url, { method: "DELETE" }).then(() =>
        this.$emit("delete", this.project.id)
      );
    },
    changeComplete() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      }).then(() => this.$emit("complete", this.project.id)).catch(err => console.log(err.message));
    },
  },
};
</script>

<style>
.projects {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: crimson;
}
.done {
  border-left: 4px solid #23e900;
}
</style>
