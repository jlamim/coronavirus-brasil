<template>
  <div class="container vh-100">
    <div class="row align-items-center">
      <div class="col-12 col-md-6 text-center">
        <img src="../assets/virus.png" alt="Coronavírus no Brasil"/>
        <h1 class="text-center mt-3">Coronavírus no Brasil</h1>
        <p class="text-center lead">Estatísticas atualizadas sobre os casos de coronavírus no Brasil.</p>
        <p class="text-center mt-5">
          <b>Desenvolvido por</b>
          <br />
          <a href="https://jonathanlamim.com.br">Jonathan Lamim</a>
        </p>
        <p class="text-center">
          <b>Fonte de Dados</b>
          <br />
          <a href="https://thevirustracker.com">thevirustracker.com</a>
        </p>
      </div>
      <div class="col-12 col-md-6">
        <div class="col-12 text-center" v-if="loading">
          <b-spinner label="Loading..."></b-spinner>
          <h4>Atualizando dados...</h4>
        </div>
        <div
          class="col-12"
          v-else-if="errored"
        >
          <b-alert show variant="warning">Não foi possível obter os dados no momento. Tente novamente em instantes!</b-alert>
        </div>
        <div class="row" v-else>
          <div class="col-12 col-md-12 text-center p-4">
            <b-badge>{{ dados.total_cases }}</b-badge>
            <h4>Infectados</h4>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="warning">{{ dados.total_active_cases }}</b-badge>
            <h4>Casos Leves</h4>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="danger">{{ dados.total_serious_cases }}</b-badge>
            <h4>Casos Graves</h4>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="success">{{ dados.total_recovered }}</b-badge>
            <h4>Curados</h4>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="dark">{{ dados.total_deaths }}</b-badge>
            <h4>Mortes</h4>
          </div>
          <div class="col-12 text-center p-4">
            <h4>Hoje</h4>
            <hr>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="warning">{{ dados.total_new_cases_today }}</b-badge>
            <h4>Novos Casos</h4>
          </div>
          <div class="col-6 col-md-6 text-center p-4">
            <b-badge variant="dark">{{ dados.total_new_deaths_today }}</b-badge>
            <h4>Mortes</h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Covid19',
  data () {
    return {
      apiPath: 'https://thevirustracker.com/free-api?countryTotal=BR',
      dados: Object,
      loading: true,
      errored: false
    }
  },
  mounted () {
    this.axios
      .get(this.apiPath)
      .then(response => {
        this.dados = response.data.countrydata[0]
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => (this.loading = false))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  text-transform: uppercase;
  font-weight: bold;
}
.badge {
  font-size: 30px;
}
hr {
  color: #ffffff;
  border-color: #ffffff;
}
a {
  color: #f9b212;
}
</style>
