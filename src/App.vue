<script lang="ts">
import { defineComponent } from 'vue';
import DatePicker from 'vue-datepicker-next';
import { format, parse } from 'date-format-parse';

export default defineComponent({
  components: {
    DatePicker,
  },
  data() {
    return {
      inputProps: {
        clearable: false,
        editable: false,
        placeholder: 'test placeholder',
        inputAttr: {
          name: 'test',
          id: 'test',
        },
      },
      shortcuts: [
        {
          text: 'range',
          onClick() {
            return [new Date(), new Date()];
          },
        },
      ],
      value: new Date(),
      append: false,
      rangeValue: [new Date(new Date().getTime() - 86400 * 1000 * 3), new Date(new Date().getTime() - 86400 * 1000)],
      formatter: {
        stringify(date: Date) {
          return format(date, 'DD/MMM/YYYY');
        },
        parse(value: string) {
          return parse(value, 'DD/MMM/YYYY');
        },
        getWeek(date: Date) {
          return date.getDate();
        },
      },
    };
  },
  computed: {
    today() {
      let date = new Date()

      date.setHours(0)
      date.setMinutes(0)
      date.setSeconds(0)
      // date.setMilliseconds(0)

      return date
    }
  },
  methods: {
    handleChange() {
      console.log('change');
    },
    handleUpdate(val: Date) {
      this.value = val;
    },
  },
})
</script>
<template>
  <div>
    <button @click="append = !append">ass</button>
    <DatePicker
      v-model:value="value"
      v-bind="inputProps"
      :clearable="false"
      :append-to-body="append"
      type="datetime"
      :time-picker-options="{ start: '00:00', end: '09:00', step: '00:30' }"
      :disabled-date="(date) => date < new Date(2021, 10, 9)"
      :open="true"
    ></DatePicker>
    <DatePicker
      v-model:value="rangeValue"
      :append-to-body="false"
      range
      :disabled-date="(date) => date < today"
      :shortcuts="shortcuts"
      :editable="false"
    ></DatePicker>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* color: #2c3e50; */
  margin-top: 60px;
  margin-left: 60px;
}
</style>
