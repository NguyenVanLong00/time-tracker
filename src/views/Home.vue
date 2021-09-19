<template>
    <el-row justify="center" class="home">
      <el-col :span="4" class="sidebar">
        <user @changeTime="changeTime" :time="time"></user>
      </el-col>
      <el-col :span="12">
        <div v-if="noData">no data</div>
        <el-row :gutter="32" v-else style="margin-bottom:-32px">
          <el-col :span="8" v-for="subject in subjects" :key="subject">
            <track-item :subject="subject" :time="time"></track-item>
          </el-col>
        </el-row>
      </el-col>
    </el-row>  
</template>

<script>
import TrackItem from "../components/TrackItem.vue";
import User from "../components/User.vue";
export default {
  components: {
    TrackItem,
    User
  },
  data() {
    return {
      subjects: null,
      time: "daily",
    };
  },
  mounted() {
    this.getSubject();
  },
  computed: {
    noData() {
      return this.subjects == null;
    },
  },
  methods: {
    async getSubject() {
      try {
        let response = await fetch("http://localhost:3000/subject");
        if (!response.ok) {
          throw Error("can't get data");
        }
        this.subjects = await response.json();
      } catch (err) {
        console.log(err.message);
      }
    },
    changeTime(time){
      this.time = time;
    }
  },
};
</script>

<style>
.home{
  margin-top:10rem;
}
.sidebar{
  margin-right:32px;
}
</style>