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
          <q-input filled v-model="date">
            <template v-slot:prepend>
              <q-icon name="event" class="cursor-pointer">
                <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                  <q-date v-model="date" mask="DD.MM.YYYY">
                    <div class="row items-center justify-end">
                      <q-btn v-close-popup label="Обновить" color="primary" flat @click="CallsPerDay(date)"/>
                    </div>
                  </q-date>
                </q-popup-proxy>
              </q-icon>
            </template>
          </q-input>
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
  <div><!-- Разделитель -->
    <q-separator class="q-mt-xl"/>
  </div>

  <div class="row section q-mt-xl disFlex">
    <div class="col-12 col-md-12 col-ml-md">
      <p class="MidFont brandgrey">Работа колл-центра</p>
    </div>
    <div class="col-6 col-md-2 col-lg-2 q-ml-md">
      <q-input filled v-model="date">
        <template v-slot:prepend>
          <q-icon name="event" class="cursor-pointer">
            <q-popup-proxy cover transition-show="scale" transition-hide="scale">
              <q-date v-model="date" mask="DD.MM.YYYY">
                <div class="row items-center justify-end">
                  <q-btn v-close-popup label="Обновить" color="primary" flat @click="CallsPerDay(date)"/>
                </div>
              </q-date>
            </q-popup-proxy>
          </q-icon>
        </template>
      </q-input>
    </div>
  </div>

  <div class="row section q-mt-xl q-ml-md">
    <div class="col-12 col-md-6">
      <div class="row disFlex">
        <div class="col-12 col-md-4 q-mt-lg">
          <p class="ttlcll">{{callsPerDay.totalcalls}}</p>
          <p class="callName">Общее количество звонков</p>
        </div>
        <div class="col-12 col-md-4 q-mt-lg">
          <p class="ttlcll">{{callsPerDay.totalleads}}</p>
          <p class="callName">Общее количество лидов</p>
        </div>
        <div class="col-12 col-md-4 q-mt-lg">
          <p class="ttlcll">{{callsPerDay.totalgreenzone}}</p>
          <p class="callName">Передано в зеленую зону</p>
        </div>

        <div class="col-12 col-md-12 q-mt-lg">
          <p class="headd">Всего</p>
        </div>

        <div class="col-md-4 q-mt-lg">
            <p class="ttlcll">{{totalCalls.totalcalls}}</p>
            <p class="callName">Общее количество звонков</p>
        </div>
        <div class="col-md-4 q-mt-lg">
            <p class="ttlcll">{{totalCalls.totalleads}}</p>
            <p class="callName">Общее количество лидов</p>
        </div>
        <div class="col-md-4 q-mt-lg">
            <p class="ttlcll">{{totalCalls.totalgreenzone}}</p>
            <p class="callName">Передано в зеленую зону</p>
        </div>
      </div>
    </div>

    <div class="col-12 col-md-6 q-mt-lg q-px-lg bg-LPink">
      <div class="row disFlex">
        <div class="col-12 q-mt-lg">
          <p class="indiText">
            Добавление в реестры и официальный перечень площадок субсидий
          </p>
        </div>
        <div class="col-6 q-mt-lg">
          <p class="indiPinkText">{{ reestrSum.mik_participants }}</p>
          <p class="callName">Участники МИК</p>
        </div>
        <div class="col-6 q-mt-lg">
          <p class="indiPinkText">{{ reestrSum.reestr_soc }}</p>
          <p class="callName">Заявки на вступление в реестр соц.предприятий</p>
        </div>
        <div class="col-6 q-mt-lg">
          <p class="indiPinkText">{{ reestrSum.list_ploshadki }}</p>
          <p class="callName">Заявки на добавление в список площадок</p>
        </div>
        <div class="col-6 q-mt-lg">
          <p class="indiPinkText">{{ reestrSum.req_approved }}</p>
          <p class="callName">Одобрено заявок</p>
        </div>
      </div>
    </div>
  </div>

</div>
</template>

<script>
// import { api } from 'boot/axios'
// import { colors } from 'quasar'
import { defineComponent, ref } from 'vue'
// import { date } from 'quasar'
import budgetTotal from './BudgetTotal.vue'
import docPrepared from './DocPrepared.vue'

export default defineComponent({
  components: { budgetTotal, docPrepared },
  name: 'PageIndex',

  setup () {
    return {
      date: ref('20.05.2020')
    }
  },

  data () {
    return {

      alleads: [],
      alleadssigned: [],
      alleadsgiven: [],

      specialist: [],
      docpreparedtotal: [],

      callsPerDay: [],
      totalCalls: [],

      reestrSum: []
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

    await this.$axios
      .get('https://mec.standsystematic.ru/api/leads/calls/greenzone/day/' + this.date)
      .then(response => {
        this.callsPerDay = response.data
      })
      .catch(error => console.log('Error', error.message))
    await this.$axios
      .get('https://mec.standsystematic.ru/api/leads/calls/greenzone')
      .then(response => {
        this.totalCalls = response.data
      })
      .catch(error => console.log('Error', error.message))

    await this.$axios
      .get('https://mec.standsystematic.ru/api/leads/mik/reestr/sum')
      .then(response => {
        this.reestrSum = response.data
      })
      .catch(error => console.log('Error', error.message))
  },

  methods: {
    CallsPerDay (newDate) {
      this.date = newDate
      this.$axios
        .get('https://mec.standsystematic.ru/api/leads/calls/greenzone/day/' + this.date)
        .then(response => {
          this.callsPerDay = response.data
        })
        .catch(error => console.log('Error', error.message))
    }
  }

})

</script>

<style lang="sass">
  td:first-child
    /* https://mec.standsystematic.ru/api/leads/mik/reestr/sum */
    color: #ff4261 !important

  .q-table__top,
  thead tr:first-child th
    background-color: #ff4261

  .q-separator
    background-color: #808080
</style>
