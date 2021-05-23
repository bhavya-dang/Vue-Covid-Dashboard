<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">
      {{ text }}
    </h2>
    <div class="text-2xl mt-4">
      {{ dateFormat }}
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Title",
  props: ["text", "date"],
  computed: {
    dateFormat: function() {
      return moment(this.date).format("MMMM Do YYYY, h:mm:ss a");
    },
  },
};
</script>
