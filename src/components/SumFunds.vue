<template>
<q-page>
  <div class="row section q-mt-lg"><!--Данные к "Текущий объем средств к выдаче"-->
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
  </div>
  <div class="col-12 col-md-8">
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
        КОНОПКА
      </div>
      <div class="col-12"><!--Диаграмма-->

      </div>
    </div>
  </div>
</q-page>
</template>

<script>
// import Chart from 'components/Chart'

export default {
  name: 'SumFunds',
  // components: { Chart },
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
    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/signed')
      .then(response => {
        this.alleadssigned = response.data
      })
    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/alleads/given')
      .then(response => {
        this.alleadsgiven = response.data
      })
      .catch(error => console.log('Error', error.message))
  }
}
</script>
