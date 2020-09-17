<template>
  <div id="app">
    <router-view
    :options="calendarArr" 
    class="calendar" 
    @handleClickDay="handleClickDay" 
    @handlePrevMonth="handlePrevMonth"
    @handleNextMonth="handleNextMonth"
    />
  </div>
</template>
<script>
import datePicker from './Date'
export default {
  name: 'date-picker',
  data () {
    return {
      calendarArr: {
          type: 'combination',
          headStyle: {
            todayBtn: 'right',
            combination: 'center',
            checkBtn: 'right',
          },
          viewStyle: {
            day: 'right'
          },
          calendarData: []
        },
    }
  },
  components: {
    datePicker
  },
  methods: {
    handleClickDay () {
    },
    handlePrevMonth () {
    },
    handleNextMonth () {
      
    }
  }
}
</script>