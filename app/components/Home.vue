<template>
  <Page>
    <ActionBar :title="year + ' ' + month" />
    <DockLayout backgroundColor="#272727">
      <FlexboxLayout
        dock="top"
        justifyContent="space-between"
        width="100%"
        backgroundColor="#272727"
      >
        <button
          text="Назад"
          @tap="back()"
        ></button>
        <button
          text="Сегодня"
          v-if="!isCurrentMonth"
          @tap="today()"
        ></button>
        <button
          text="Вперед"
          @tap="forward()"
        ></button>
      </FlexboxLayout>
      <FlexboxLayout flexWrap="wrap" backgroundColor="#272727">
        <label
          v-for="day in days"
          :key="day"
          style="border-width: 1px; border-color: #333333;"
          :backgroundColor="isCurrentDay(day) ? '#48494a' : '#272727'"
          :text="day + 1"
          :width="100 / 7 + '%'"
          height="50px"
        />
      </FlexboxLayout>
    </DockLayout>
  </Page>
</template>

<script>
import moment from "moment";

export default {
  data() {
    return {
      offset: 0, // переменная сдвига по месяцам
      months: [
        "Январь",
        "Февраль",
        "Март",
        "Апрель",
        "Май",
        "Июнь",
        "Июль",
        "Август",
        "Сентябрь",
        "Октябрь",
        "Ноябрь",
        "Декабрь",
      ],
    };
  },
  computed: {
    days() {
      return [
        ...Array(moment().add(this.offset, "months").daysInMonth()).keys(),
      ];
    },
    isCurrentMonth() {
      return this.offset == 0;
    },
    month() {
      return this.months[moment().add(this.offset, 'months').month()];
    },
    year() {
      return moment().add(this.offset, "months").year();
    },
  },
  methods: {
    forward() {
      this.offset = this.offset + 1;
    },
    today() {
      this.offset = 0;
    },
    back() {
      this.offset = this.offset - 1;
    },
    isCurrentDay(day) {
      return (moment().date() - 1) == day && this.isCurrentMonth;
    },
  },
};
</script>
