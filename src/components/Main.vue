<template>
  <div class="select-test center con-selects">
    <div class="controls grid">
      <vs-row>
        <vs-col w="12" vs-justify="left">
          <h1>My stack</h1>
        </vs-col>
      </vs-row>
      <vs-row>
        <vs-col vs-type="flex" w="4">
          <vs-select placeholder="Focus" v-model="focusId">
            <vs-option v-for="(item, index) in params.focus"
                       :label="item.name"
                       :key="index"
                       :value="String(index)"
            >
              {{item.name}}
            </vs-option>
          </vs-select>
        </vs-col>

        <vs-col vs-type="flex" vs-justify="left" w="4">
          <vs-select placeholder="Technology" v-model="technologyId" :key="focusId" :disabled="focusId ? false : true">
            <template v-if="focusId">
              <vs-option v-for="(item, index) in params.focus[focusId].technologies"
                         :label="item.name"
                         :key="index"
                         :value="String(index)"
              >
                {{item.name}}
            </vs-option>
            </template>
          </vs-select>
        </vs-col>

        <vs-col vs-type="flex" vs-justify="left" w="4">
          <vs-select placeholder="Scope" v-model="scopeId" :key="technologyId" :disabled="technologyId ? false : true">
            <template v-if="technologyId">
              <vs-option v-for="(item, index) in params.focus[focusId].technologies[technologyId].scope"
                         :label="item.name"
                         :key="index"
                         :value="String(index)"
              >
                {{item.name}}
              </vs-option>
            </template>
          </vs-select>
        </vs-col>
      </vs-row>
    </div>
    <chart :data="chartData" :key="focusId/scopeId"></chart>
  </div>
</template>

<script>
  import jsonData from '../data.json'
  import Chart from "@/components/Chart";

  export default {
  name: 'Main',
  components: {Chart},

  data() {
    return {
      params: {},
      focusId: '',
      technologyId: '',
      scopeId: '',
    }
  },
  computed: {
    chartData() {
      return {
        focus: this.focusId != '' ? this.params.focus[this.focusId].experience : [],
        scope: this.scopeId != '' ? this.params.focus[this.focusId]
          .technologies[this.technologyId].scope[this.scopeId].experience : []
      }
    }
  },
  watch: {
    focusId: function () {
      this.technologyId = '';
      this.scopeId = '';
    },
    technologyId: function () {
      this.scopeId = '';
    }
  },
  created() {
    this.params = jsonData;
  }
}
</script>

<style>
  .controls {
    background-color: rgb(var(--vs-dark));
    padding: 20px;
  }
  h1 {
    color: #fff;
  }
</style>
