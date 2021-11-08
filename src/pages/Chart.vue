<template>
  <div class="row section q-mt-lg" style="display:flex">

  </div>
</template>

<script>

export default {
  data () {
    return {
      budgetAll: []
    }
  },
  mounted () {
    this.$axios
      .get('https://mec.standsystematic.ru/api/budget/total/day/27.10.2021')
      .then(response => {
        this.budgetAll = response.data
      })
      .catch(error => console.log('Error', error.message))
  }
}
</script>
