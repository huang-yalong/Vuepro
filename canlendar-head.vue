<template>
  <div class="calendar-header clear">
    <div class="calendar-box" v-if="this.headOptions.type == 'combination'">
      <div class="calendar-content" :style="{'text-align': this.headStyle.combination}">
        <span class="calendar-prev" @click="handlePrevMonth"></span>
        <span class="calendar-headDate"> {{this.headOptions.date}} </span>
        <span class="calendar-next" @click="handleNextMonth"></span>
      </div>
      <span class="calendar-today" @click="handleToday()"> 今天 </span>
    </div>
    <div class="calendar-box" v-else>
      <span class="calendar-headDate"> {{this.headOptions.date}} </span>
      <span class="calendar-today dispersion-today" :style="{float: this.headStyle.todayBtn}" @click="handleToday()"> 今天 </span>
      <div class="calendar-content dispersion" :style="{float: this.headStyle.checkBtn}">
        <span class="calendar-prev" @click="handlePrevMonth"></span>
        <span class="calendar-next" @click="handleNextMonth"></span>
      </div>
     
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      headOptions: Object
    },
    data () {
      return {
        headStyle: ''
      }
    },
    mounted() {
      this.headStyle = this.headOptions.style;
    },
    methods: {
      // 上一个月
      handlePrevMonth () {
        this.$emit('handlePrevMonth');
      },
      // 下一个月
      handleNextMonth () {
        this.$emit('handleNextMonth');
      },
      // 回到今天
      handleToday () {
        this.$emit('handleToday');
      }
    }
  }
</script>