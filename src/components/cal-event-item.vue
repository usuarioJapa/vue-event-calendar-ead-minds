<template>
<div class="wrapper"
     :class="[
        (!event || (event.classStatus == 'F')) ? 'finished' :
        ((event.date == today) && event.title.includes('Unit')) ? 'other' :
        event.title.includes('Unit') ? 'lab' : 'conversation'
    ]">
  <div class="time">
    <!-- <p>{{dateTimeFormatter(Date.parse(new Date(event.date)),i18n[locale].fullFormat)}}</p> -->
    <p>{{ event ? event.time : '' }}</p>
  </div>
  <div class="day">
    <!-- <p>{{dateTimeFormatter(Date.parse(new Date(event.date)),i18n[locale].fullFormat)}}</p> -->
    <p>{{ event ? event.date : '' }}</p>
  </div>
  <div class="title">
    <p>{{ event ? event.title : '' }}</p>
  </div>

</div>
</template>

<script>
import i18n from '../i18n.js'
import { dateTimeFormatter } from '../tools.js'
export default {
  data() {
    return {
      i18n
    }
  },
  props: {
    event: {
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    locale: {
      type: String,
      required: true
    }
  },
  computed: {
    today() {
      let date = new Date()
      return `${date.getUTCFullYear()}/${(date.getUTCMonth() + 1) > 9 ? (date.getUTCMonth() + 1) : `0${date.getUTCMonth() + 1}` }/${date.getUTCDate() > 9 ? date.getUTCDate() : `0${date.getUTCDate()}`}`
    }
  },
  methods: {
    dateTimeFormatter
  }
}
</script>

<style lang="scss" scoped>
  .wrapper {
    align-items: center;
  }

  .time, .day, .title {
    height: 25px;
  }
  .time {
    width: 56px;
  }
  .day {
    width: 87px;
  }
</style>
