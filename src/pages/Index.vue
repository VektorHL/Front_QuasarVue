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

  <div class="row section q-mt-lg"><!--Данные к "Текущий объем средств к выдаче"-->
    <div class="col-12 col-md-4 col-lg-3 line"><!--Основные цифры-->
      <div class="col q-mt-lg"> <!--Одобрено заявок. Данные-->
          <p class="headd">Одобрено заявок</p>
          <p class="summ">{{alleads.totalcount}}</p>
          <p class="total line">{{alleads.totalsum}} млн</p>
      </div>
      <div class="col q-mt-lg"> <!--Заключено соглашений. Данные-->
          <p class="headd">Заключено соглашений</p>
          <p class="summ">{{alleadssigned.totalcount}}</p>
          <p class="total line">{{alleadssigned.totalsum}} млн</p>
      </div>
      <div class="col q-mt-lg"> <!--Получили средства на счет. Данные-->
          <p class="headd">Получили средства на счет</p>
          <p class="summ">{{alleadsgiven.totalcount}}</p>
          <p class="total">{{alleadsgiven.totalsum}} млн</p>
      </div>
    </div>
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
          КОНОПКА
        </div>
        <div class="col-12"><!--Диаграмма-->

        </div>
      </div>
    </div>
  </div>

  <div class="row section q-mt-xl"><!-- Потенциальный объем средств к выдаче. Разделитель -->
    <div class="col-auto subtitle ">
      <p class="subtitle">Потенциальный объем средств к выдаче</p>
    </div>
    <div class="col">
      <q-separator class="q-ml-sm q-mt-md bg-grey" />
    </div>
  </div>

  <div class="row section q-mt-lg"><!--Данные к "Потенциальный объем средств к выдаче"-->
    <div class="col-12 col-md-4 col-lg-3 q-mr-lg line"><!--Основные цифры-->
      <div class="col q-mt-lg"> <!--Заявки в Департаменте. Данные-->
          <p class="headd">Заявки в Департаменте</p>
          <p class="summ">{{specialist.totalcount}}</p>
          <p class="total">{{specialist.totalsum}} млн</p>
      </div>
      <div class="col q-mt-xl documents"> <!--Готовят документы. Данные-->
          <p class="headd">Готовят документы</p>
          <p class="summ">{{docpreparedtotal.totalcount}}</p>
          <p class="total">предпринимателей</p>
      </div>
    </div>
    <div class="col-12 col-md-7"><!--Таблицы-->
      <div class="col q-mt-lg"><!--Таблица 1-->
        <budget-total />
      </div>
      <div class="col q-mt-lg"><!--Таблица 2-->
        <doc-prepared />
      </div>
    </div>
  </div>
  <!-- <sum-funds /> -->

</div>
</template>

<script>
// import { api } from 'boot/axios'
// import { colors } from 'quasar'
import { defineComponent } from 'vue'
import budgetTotal from './BudgetTotal.vue'
import docPrepared from './DocPrepared.vue'

export default defineComponent({
  components: { budgetTotal, docPrepared },
  name: 'PageIndex',
  data () {
    return {
      alleads: [],
      alleadssigned: [],
      alleadsgiven: [],

      specialist: [],
      docpreparedtotal: []
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

    await this.$axios
      .get('https://mec.standsystematic.ru/api/budget/specialist')
      .then(response => {
        this.specialist = response.data
      })
      .catch(error => console.log('Error', error.message))
    await this.$axios
      .get('https://mec.standsystematic.ru/api/leads/docprepared/total')
      .then(response => {
        this.docpreparedtotal = response.data
      })
      .catch(error => console.log('Error', error.message))
  }
})
</script>

<style lang="sass">
  td:first-child
    /* bg color is important for td; just specify one */
    color: #ff4261 !important

  .q-table__top,
  thead tr:first-child th
    /* bg color is important for th; just specify one */
    background-color: #ff4261
</style>
