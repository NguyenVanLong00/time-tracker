<template>
  <div class="tracker-item" :class="subjectClass">
    <img :src="subjectIcon" class="icon" />
    <div class="tracker-content">
      <div class="header">
        <div class="tracker-title font-18">{{ subject.title }}</div>
        <div class="ellipsis">
          <img :src="ellipsis" alt="ellipsis" />
        </div>
      </div>
      <div class="main">
        <h3 class="current-time">{{ subjectCurrentTime }} hrs</h3>
        <p class="last-time">last {{ subjectLastTime }} hrs</p>
      </div>
    </div>
  </div>
</template>

<script>
import ellipsis from "../assets/images/icon-ellipsis.svg";

import exercise from "../assets/images/icon-exercise.svg";
import play from "../assets/images/icon-play.svg";
import self_care from "../assets/images/icon-self-care.svg";
import social from "../assets/images/icon-social.svg";
import study from "../assets/images/icon-study.svg";
import work from "../assets/images/icon-work.svg";

export default {
  props: ["subject", "time"],
  data() {
    return {
      ellipsis,
      exercise,
      play,
      self_care,
      social,
      study,
      work,
    };
  },
  mounted() {},
  computed: {
    subjectClass() {
      if (this.subject.title.toLowerCase() == "self care")
        return "bg-self-care";
      return "bg-" + this.subject.title.toLowerCase();
    },
    subjectCurrentTime() {
        let timeframe = this.subject.timeframes;
      switch (this.time) {
        case "daily":
          return timeframe.daily.current;
        case "weekly":
          return timeframe.weekly.current;
        case "monthly":
          return timeframe.monthly.current;
      }
    },
    subjectLastTime() {
        let timeframe = this.subject.timeframes;
      switch (this.time) {
        case "daily":
          return 'day - ' + timeframe.daily.previous;
        case "weekly":
          return 'week - ' + timeframe.weekly.previous;
        case "monthly":
          return 'month - ' + timeframe.monthly.previous;
      }
    },
    subjectIcon() {
      switch (this.subject.title.toLowerCase()) {
        case "exercise":
          return this.exercise;
        case "play":
          return this.play;
        case "self care":
          return this.self_care;
        case "social":
          return this.social;
        case "study":
          return this.study;
        case "work":
          return this.work;
      }
    },
  },
};
</script>

<style lang="scss">
.tracker-item {
  position: relative;
  padding-top: 48px;
  margin-bottom: 32px;
  border-radius: 12px;
}


.tracker-content {
  position: relative;
  background-color: hsl(235, 46%, 20%);
  z-index: 2;
  padding: 42px 32px;
  border-radius: 10px;
  transition: 0.2s;
  .header {
    display: flex;
    justify-content: space-between;
  }
}
.tracker-content:hover {
  background-color: lighten($color: hsl(235, 46%, 20%), $amount: 10);
}
.icon {
  position: absolute;
  top: 6px;
  right: 8px;
  width: 62px;
  z-index: 1;
}
.ellipsis {
  cursor: pointer;
}
.current-time {
    margin-top:24px;
    font-size:64px;
    font-weight:300;
}
.last-time {
    margin-top:12px;
    font-weight: 300;
    opacity: 60%;
    font-size: 12px;
}
</style>