<script>
import { format } from "date-fns";

export default {
  props: {
    dayData: {
      type: Date,
      required: true,
    },

    events: {
      type: Array,
      required: true,
    },

    isPreviousMonth: {
      type: Boolean,
      required: true,
    },

    isSelectedDay: {
      type: Boolean,
      required: true,
    },
  },

  methods: {
    formatDate(date, formatStr) {
      return format(date, formatStr);
    },

    handleClick() {
      this.$emit("click", this.dayData);
    },
  },
};
</script>

<template>
  <div
    class="item"
    :class="{ 'previous-month': isPreviousMonth, selected: isSelectedDay }"
    @click="handleClick"
  >
    {{ formatDate(dayData, "d") }}
    <div v-if="events.length" class="item__event">
      <p v-for="event in events" :key="event.start" class="item__title">
        {{ event.title }}
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.item {
  position: relative;
  display: flex;
  justify-content: flex-start;
  align-items: end;
  height: 50px;
  padding: 10px;
  font-size: 16px;
  cursor: pointer;
  background-color: #2d2e34;
  border-radius: 4px;
  color: #d1d1d1;
  user-select: none;
  transition: background-color ease-in 300ms;

  &__event {
    position: absolute;
    top: 5px;
    right: 5px;
    width: 12px;
    height: 12px;
    font-size: 0px;
    border-radius: 50%;
    background-color: #318eb1;
  }

  &__title {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }

  &:hover {
    opacity: 0.8;
  }
}

.selected {
  background-color: #303d4f;
}

.previous-month {
  color: #595959;
}

@media (min-width: 768px) {
  .item {
    height: 60px;

    &__event {
      width: 50px;
      height: auto;
      line-height: 1;
      padding: 5px;
      font-size: 14px;
      border-radius: 10px;
    }
  }
}
</style>
