<template>
  <div class="user">
    <div class="user-header">
      <div class="avatar">
        <img :src="avatar" />
      </div>
      <div class="main">
        <p>Report for</p>
        <h3>Jemremy Robson</h3>
      </div>
    </div>
    <div class="user-nav">
      <el-button
        type="text"
        class="custom-btn"
        :class="{ 'active-btn': time == 'daily' }"
        @click="changeTime('daily')"
        >Daily</el-button
      >
      <el-button
        type="text"
        class="custom-btn"
        :class="{ 'active-btn': time == 'weekly' }"
        @click="changeTime('weekly')"
        >Weekly</el-button
      >
      <el-button
        type="text"
        class="custom-btn"
        :class="{ 'active-btn': time == 'monthly' }"
        @click="changeTime('monthly')"
        >Monthly</el-button
      >
    </div>
  </div>
</template>

<script>
import avatar from "../assets/images/image-jeremy.png";
export default {
  props: {
    time: String,
  },
  data() {
    return {
      avatar,
    };
  },
  methods: {
      changeTime(time){
          this.$emit('changeTime',time);
      }
      
  },
};
</script>

<style lang="scss">
.user {
  background-color: hsl(235, 46%, 20%);
  border-radius: 12px;
  height: 100%;
  .main {
    margin-top: 32px;
    margin-bottom: 64px;
    p {
      font-size: 14px;
      font-weight: 300;
      opacity: 60%;
    }
    h3 {
      font-size: 52px;
      font-weight: 300;
    }
  }
}
.user-header {
  padding: 42px 32px;
}
.user-header {
  background-color: hsl(246, 80%, 60%);
  border-radius: 12px;
}
.avatar {
  width: 78px;
  img {
    width: 100%;
    border-radius: 50%;
    border: 3px solid #fff;
  }
}
.user-nav {
  padding: 24px 32px;
  .custom-btn {
    display: block;
    margin-left: 0px;
    color: currentColor;
    font-size: 18px;
    font-weight: 300;
    opacity: 0.6;
    &:hover {
      opacity: 1;
      color: currentColor;
    }
  }
  .active-btn {
    opacity: 1;
  }
}
</style>