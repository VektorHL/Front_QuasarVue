<template>
<div class="q-pa-md q-ml-sm q-mt-xl">
  <div class="row title"><!-- Основные показатели -->
    <div class="col-12" >
      <p class="title">Основные показатели
        <br>
        о ходе субсидийной кампании</p>
    </div>
  </div>
  <div class="row section q-mt-lg q-mb-xl"><!-- Текущий объем средств к выдаче. Разделитель -->
    <div class="col-auto subtitle ">
        <p class="subtitle">Текущий объем средств к выдаче</p>
    </div>
    <div class="col">
      <q-separator class="q-ml-sm q-mt-md bg-grey" />
    </div>
  </div>

  <div class="row section q-mt-lg">
    <div class="col-12 col-md-4 col-lg-3 line">
      <div class="col q-mt-lg">
          <p class="headd">Одобрено заявок</p>
          <p class="summ">{{alleads.totalcount}}</p>
          <p class="total line">{{alleads.totalsum}} млн</p>
      </div>
      <div class="col q-mt-lg">
          <p class="headd">Заключено соглашений</p>
          <p class="summ">{{alleadssigned.totalcount}}</p>
          <p class="total line">{{alleadssigned.totalsum}} млн</p>
      </div>
      <div class="col q-mt-lg">
          <p class="headd">Получили средства на счет</p>
          <p class="summ">{{alleadsgiven.totalcount}}</p>
          <p class="total">{{alleadsgiven.totalsum}} млн</p>
      </div>
      </div>
        <div class="col-12 col-md-8">
      <div class="row ">
        <div class="col-12 col-md-6 q-ml-lg">
          <p class="chart_title">
            Объем выданных средств Департаментом
            <br>
            по каждой субсидии и количество
            <br>
            предпринимателей-получателей
          </p>
        </div>
        <div class="cil-12 q-md-5">
          КОНОПКА
        </div>
        <div class="col-12">

        </div>
      </div>
    </div>
  </div>

  <!-- <sum-funds /> -->

</div>
</template>

<script>
import { defineComponent } from 'vue'
// import SumFunds from 'components/SumFunds'
// import Chart from 'components/Chart'
// import Chart from 'src/components/Chart.vue'
// import SumFunds from 'src/components/SumFunds.vue'

export default defineComponent({
  // components: { SumFunds },
  name: 'PageIndex',
  data () {
    return {
      alleads: [],
      alleadssigned: [],
      alleadsgiven: []
    }
  },
  async mounted () {
    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/alleads')
      .then(response => {
        this.alleads = response.data
      })
      .catch(error => console.log('Error', error.message))
    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/signed')
      .then(response => {
        this.alleadssigned = response.data
      })
      .catch(error => console.log('Error', error.message))
    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/given')
      .then(response => {
        this.alleadsgiven = response.data
      })
      .catch(error => console.log('Error', error.message))
  }
})
</script>
