<template>
  <div class="container mt-3">
    <h3>Showing {{filteredIssues.length}} of {{reportData.length}} total issues</h3>
    <div class="row">
      <div class="col-8">
        <b-card class="mb-2" v-for="(issue, index) in filteredIssues" :key="index">
          <p>Type: {{issue.type}}</p>
          <p>Check Name: {{issue.check_name}}</p>
          <p>Description: {{issue.description}}</p>
          <p>Categories: {{issue.categories}}</p>
          <p>Path: {{issue.location.path}}</p>
          <p
            v-if="issue.location.hasOwnProperty('positions')"
          >Line: {{issue.location.positions.begin.line}} Column: {{issue.location.positions.begin.column}}</p>
        </b-card>
      </div>
      <div class="col-4">
        <b-form-group label="SEVERITY">
          <b-form-checkbox-group
            id="severities-checkbox-group-1"
            v-model="selectedSeverities"
            :options="severities"
            name="severities-1"
          ></b-form-checkbox-group>
        </b-form-group>

        <b-form-group label="CATEGORY">
          <b-form-checkbox-group
            id="categories-checkbox-group-1"
            v-model="selectedCategories"
            :options="categories"
            name="categories-1"
          ></b-form-checkbox-group>
        </b-form-group>
      </div>
    </div>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: ["reportData"],
  data() {
    return {
      severities: [],
      selectedSeverities: [],
      categories: [],
      selectedCategories: []
    };
  },
  computed: {
    filteredIssues: function() {
      let issues = this.reportData;

      if (this.selectedSeverities.length > 0) {
        issues = _.filter(issues, item => {
          if (item.severity.includes(this.selectedSeverities)) {
            return item;
          }
        });
      }

      if (this.selectedCategories.length > 0) {
        issues = _.filter(issues, item => {
          if (
            this.hasSelectedCategory(item.categories, this.selectedCategories)
          ) {
            return item;
          }
        });
      }

      return issues;
    }
  },
  methods: {
    hasSelectedCategory(categories, selectedCategories) {
      for (var i = 0; i < categories.length; i++) {
        if (selectedCategories.includes(categories[i])) {
          return true;
        }
      }
    }
  },
  mounted() {
    this.severities = _.uniq(_.map(this.reportData, "severity"));
    this.categories = _.uniq(_.flatMap(_.map(this.reportData, "categories")));
  }
};
</script>

<style>
</style>