<template>
  <q-page>
    <!-- <div class="row section">
      <div class="col-12 subtitle ">
          <p class="subtitle">Текущий объем средств к выдаче</p>
      </div>
      <div class="col">
        <q-separator class="q-ml-sm q-mt-md bg-grey" />
      </div>
    </div> -->
    <div class="row section q-mt-lg">
      <div class="col-12 col-md-4 col-lg-3 line">
        <div class="col q-mt-lg">
          <h5 class="MidFont brandgrey">Одобрено заявок</h5>
          <p class="">{{alleads.totalcount}}</p>
          <p class="">{{alleads.totalsum}}</p>
        </div>
        <div class="col q-mt-lg">
          <h5 class="MidFont brandgrey">Заключено соглашений</h5>
          <p class="">{{alleadssigned.totalcount}}</p>
          <p class="">{{alleadssigned.totalsum}}</p>
        </div>
        <div class="col q-mt-lg">
          <h5 class="MidFont">Получили средства на счет</h5>
          <p class="">{{alleadsgiven.totalcount}}</p>
          <p class="">{{alleadsgiven.totalsum}}</p>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'SumFunds',
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
