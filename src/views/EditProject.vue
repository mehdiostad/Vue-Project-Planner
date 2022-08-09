<template>
  <form @submit.prevent="handleEdit">
    <label>Title:</label>
    <input type="text" required v-model="title" />
    <label>Details:</label>
    <textarea v-model="details"></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => {
        this.details = data.detail;
        this.title = data.title;
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleEdit() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          details: this.details,
        }),
      })
        .then(() => this.$router.push("/"))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style></style>
