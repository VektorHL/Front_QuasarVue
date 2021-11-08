<template>
    <div class="col-12 col-md-8"><!--Объем выданных средств. Кнопка даты. Диаграмма-->
        <div class="row ">
          <div class="col-12 col-md-6 q-ml-lg"><!--Объем выданных средств-->
            <p class="chart_title">
              Объем выданных средств Департаментом
              <br>
              по каждой субсидии и количество
              <br>
              предпринимателей-получателей
            </p>
          </div>
          <div class="cil-12 q-md-5"><!--Кнопка-->
            <q-input filled v-model="date">
              <template v-slot:prepend>
                <q-icon name="event" class="cursor-pointer">
                  <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                    <q-date v-model="date" mask="DD.MM.YYYY">
                      <div class="row items-center justify-end">
                        <q-btn v-close-popup label="Обновить" color="primary" flat @click="changeCharts(date)"/>
                      </div>
                    </q-date>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>
          <div class="col-12 col-md-8"><!--Диаграмма-->
            <div class="row disFlex">
              <div class="row section q-mt-lg" style="display:flex">
                <div class="hello" ref="chartdiv1">
                </div>
                <div class="hello" ref="chartdiv2">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
</template>

<script >
import * as am4core from "@amcharts/amcharts4/core"
import * as am4charts from "@amcharts/amcharts4/charts"
import am4themes_animated from "@amcharts/amcharts4/themes/animated"

am4core.useTheme(am4themes_animated)

import { ref } from 'vue'

export default {
  setup () {
    return {
      date: ref('20.05.2020')
    }
  },
  data() {
    return {
      budgetAll: [] 
    }
  },
  mounted() {
    this.$axios
        .get('https://mec.standsystematic.ru/api/budget/total/day/' + this.date)
        .then(response => {
          this.budgetAll = response.data
        })
        .catch(error => console.log('Error', error.message))

    let chart1 = am4core.create(this.$refs.chartdiv1, am4charts.PieChart);

    chart1.dataSource.url = 'https://mec.standsystematic.ru/api/budget/total/day/' + this.date;

    var pieSeries = chart1.series.push(new am4charts.PieSeries());
    pieSeries.dataFields.value = "total_budget";
    pieSeries.dataFields.category = "pipename";

    pieSeries.colors.list = [
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
      am4core.color("#fabbbb"),
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
    ];


    let chart2 = am4core.create(this.$refs.chartdiv2, am4charts.PieChart);

    chart2.dataSource.url = 'https://mec.standsystematic.ru/api/budget/total/day/' + this.date;

    var pieSeries = chart2.series.push(new am4charts.PieSeries());
    pieSeries.dataFields.value = "amount";
    pieSeries.dataFields.category = "pipename";

    pieSeries.colors.list = [
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
      am4core.color("#fabbbb"),
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
    ];
  },
  methods: {
    changeCharts (newDate) {
      this.date = newDate
      let chart1 = am4core.create(this.$refs.chartdiv1, am4charts.PieChart);

      chart1.dataSource.url = 'https://mec.standsystematic.ru/api/budget/total/day/' + this.date;

      var pieSeries = chart1.series.push(new am4charts.PieSeries());
      pieSeries.dataFields.value = "total_budget";
      pieSeries.dataFields.category = "pipename";

      pieSeries.colors.list = [
        am4core.color("#FF4258"),
        am4core.color("#BF5561"),
        am4core.color("#A61526"),
        am4core.color("#FF7182"),
        am4core.color("#FF97A3"),
        am4core.color("#faa2a2"),
        am4core.color("#fabbbb"),
        am4core.color("#FF4258"),
        am4core.color("#BF5561"),
        am4core.color("#A61526"),
        am4core.color("#FF7182"),
        am4core.color("#FF97A3"),
        am4core.color("#faa2a2"),
      ];

      let chart2 = am4core.create(this.$refs.chartdiv2, am4charts.PieChart);

    chart2.dataSource.url = 'https://mec.standsystematic.ru/api/budget/total/day/' + this.date;

    var pieSeries = chart2.series.push(new am4charts.PieSeries());
    pieSeries.dataFields.value = "amount";
    pieSeries.dataFields.category = "pipename";

    pieSeries.colors.list = [
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
      am4core.color("#fabbbb"),
      am4core.color("#FF4258"),
      am4core.color("#BF5561"),
      am4core.color("#A61526"),
      am4core.color("#FF7182"),
      am4core.color("#FF97A3"),
      am4core.color("#faa2a2"),
    ];
    }
  }
}
</script>

<style scoped>
.hello {
  width: 1000px;
  height: 500px;
}
</style>
