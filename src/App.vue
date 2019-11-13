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
      <issues-list :report-data=reportData></issues-list>
    </main>
    
    <footer class="text-muted">
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
import reportdataJson from './testData/gl-code-quality-report-small.json'

export default {
  name: 'app',
  components: {
    IssuesList
  },
  data() {
    return{
      reportData: reportdataJson
    }
  }
}
</script>

<style>

</style>
