<template>
  <button @click="change">Update Status {{ statusValue }} !</button>
</template>

<script>
export default {
  name: "prompt",
  props: ["id", "status"],
  data() {
    return {
      statusValue: this.status,
    };
  },
  methods: {
    change: function() {
      // if (this.id === 0) {
      //   this.statusValue = "success";
      // } else if (this.id === 1) {
      //   this.statusValue = "pending";
      // } else {
      //   this.statusValue = "failed";
      // }
      this.$emit("change", this.statusValue);
    },
  },
};
</script>
