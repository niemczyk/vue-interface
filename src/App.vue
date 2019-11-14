<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <current-machine :item="currentMachine" v-if="currentMachine" />
    <br/><br/>
      <add-machine @add="addItem"/>
      <search-machines
        @searchMachineRecords="searchMachines"
        :myKey="filterKey"
        :myDir="filterDir"
        @requestKey="changeKey"
        @requestDir="changeDir"
        @handlePick="handlePick"
      />
      <machine-list 
        :machines="filteredApts" 
        :currentMachine="currentMachine"
        @handlePick="handlePick"
        @remove="removeItem" 
        @edit="editItem"
        />
    </div>
  </div>
</template>

<script>
import AddMachine from "./components/AddMachine";
import SearchMachines from "./components/SearchMachines";
import MachineList from "./components/MachineList";
import CurrentMachine from "@/components/CurrentMachine";
import _ from "lodash";
import axios from "axios";

export default {
  machineName: "MainApp",
  data: function() {
    return {
      machines: [],
      currentMachine: null,
      filterKey: "machineName",
      filterDir: "asc",
      searchTerms: "",
      machIndex: 0
    };
  },
  components: {
    MachineList,
    CurrentMachine,    
    SearchMachines,
    AddMachine
  },
  mounted() {
    axios.get("./data/machines.json").then(
      response =>
        (this.machines = response.data.map(item => {
          item.machId = this.machIndex;
          this.machIndex++;
          return item;
        }))
    );
  },
  computed: {
    searchedMachs: function() {
      return this.machines.filter(item => {
        return (
          item.machineName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.manufacturer.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.machineDescription.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },
    filteredApts: function() {
      return _.orderBy(
        this.searchedMachs,
        item => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDir
      );
    }
  },
  methods: {
    changeKey: function(value) {
      this.filterKey = value;
    },
    changeDir: function(value) {
      this.filterDir = value;
    },
    searchMachines: function(terms) {
      this.searchTerms = terms;
    },
    handlePick: function(payload) {
      this.currentMachine = payload;
    },
    addItem: function(mach) {
      mach.machId = this.machIndex;
      this.machIndex++;
      this.machines.push(mach);
    },
    removeItem: function(mach) {
      this.machines = _.without(this.machines, mach);
    },
    editItem: function(id, field, text) {
      const machIndex = _.findIndex(this.machines, {
        machId: id
      });
      this.machines[machIndex][field] = text;
    }
  }
};
</script>

