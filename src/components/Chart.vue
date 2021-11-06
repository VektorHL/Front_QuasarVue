<template>
  <q-page>
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
    </div>

  </q-page>
</template>

<script>

export default {
  name: 'Chart',
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
