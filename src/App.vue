<template>
  <div>
    <header>
      <div class="navbar navbar-dark bg-dark box-shadow">
        <div class="container d-flex justify-content-between">
          <a href="#" class="navbar-brand d-flex align-items-center">
            <strong>Code Climate Report Viewer</strong>
          </a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarHeader" aria-controls="navbarHeader" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
        </div>
      </div>
    </header>
    <main role="main">
      <div class="container mt-2">
        <b-btn @click="loadJson()">Load Json</b-btn>
        <b-btn class="ml-2" @click="clearJsonLoad()">Clear</b-btn>
        <b-textarea class="mt-2" v-if="showLoadJson" v-model="reportJsonString"></b-textarea>
      </div>
      <issues-list v-if="reportData" :report-data=reportData></issues-list>
    </main>
    
    <footer class="text-muted mt-5">
      <div class="container">
        <p class="float-right">
          <a href="#">Back to top</a>
        <p>Code Climate report viewer <a href="https://docs.codeclimate.com/docs">Code Climate docs</a></p>
      </div>
    </footer>
  </div>
</template>

<script>
import IssuesList from './components/IssuesList.vue'

export default {
  name: 'app',
  components: {
    IssuesList
  },
  data() {
    return{
      showLoadJson: true,
      reportJsonString: '',
      reportData: null
    }
  },
  methods: {
    loadJson() {
      this.reportData = JSON.parse(this.reportJsonString)
      this.showLoadJson = false
    },
    clearJsonLoad() {
      this.reportData = ''
      this.showLoadJson = true
    }
  }
}
</script>

<style>

</style>
