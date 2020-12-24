<template>
  <mark-line
    :markLineTime="currentTime"
    :getPositonOffset="getPositonOffset"
    color="rgba(255,0,0,.4)"
  ></mark-line>
</template>

<script>
import dayjs from "dayjs";
import MarkLine from "./index.vue";
export default {
  name: "CurrentTime",
  components: { MarkLine },
  props: {
    getPositonOffset: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      currentTime: dayjs()
        .subtract(8, "hour")
        .toString()
    };
  },
  created() {
    const timeNow = setInterval(() => {
      this.currentTime = dayjs()
        .subtract(8, "hour")
        .toString();
    }, 1000);
    this.$once("hook:beforeDestroy", () => {
      clearInterval(timeNow);
    });
  }
};
</script>
