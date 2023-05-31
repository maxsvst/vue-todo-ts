<template>
  <footer class="app-footer">
    Активных todo: {{ stats.active }}, Выполненных todo: {{ stats.done }}
  </footer>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import { Stats } from "../types/Stats";

export default defineComponent({
  props: {
    stats: {
      type: Object as PropType<Stats>,
      required: true,
    },
  },
});
</script>
