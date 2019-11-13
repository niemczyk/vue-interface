<template>
  <div class="col-12">
    <div class="card textcenter mt-3">
      <div class="card-header bg-primary text-white" @click="hidepanel=!hidepanel">
        <font-awesome-icon icon="plus" class="mr-3"/>Add Machine
      </div>

      <div class="card-body" :class="{ 'd-none': hidepanel}">
        <form id="machForm" @submit.prevent="requestAdd">
          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="machineName">Machine Name</label>
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                name="machineName"
                id="machineName"
                placeholder="Machine"
                v-model="formData.machineName"
              >
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="manufacturer">Pet Owner</label>
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                id="manufacturer"
                placeholder="Owner's Name"
                v-model="formData.manufacturer"
              >
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="machDate">Date</label>
            <div class="col-md-4">
              <input type="date" class="form-control" id="machDate" v-model="formData.machDate">
            </div>
            <label class="col-md-2 col-form-label text-md-right" for="machTime">Time</label>
            <div class="col-md-4">
              <input
                type="time"
                class="form-control"
                name="machTime"
                id="machTime"
                v-model="formData.machTime"
              >
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 text-md-right" for="machineDescription">Apt. Notes</label>
            <div class="col-md-10">
              <textarea
                class="form-control"
                rows="4"
                cols="50"
                name="machineDescription"
                id="machineDescription"
                placeholder="Machine Notes"
                v-model="formData.machineDescription"
              ></textarea>
            </div>
          </div>

          <div class="form-group form-row mb-0">
            <div class="offset-md-2 col-md-10">
              <button type="submit" class="btn btn-primary d-block ml-auto">Add Machine</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  name: "AddMachine",
  data() {
    return {
      formData: [],
      hidepanel: true
    };
  },
  components: {
    FontAwesomeIcon
  },
  methods: {
    requestAdd: function() {
      this.formData = {
        machineName: this.formData.machineName,
        manufacturer: this.formData.manufacturer,
        machDate: this.formData.machDate + " " + this.formData.machTime,
        machineDescription: this.formData.machineDescription
      };
      this.$emit("add", this.formData);
      this.formData = [];
      this.hidepanel = true;
    }
  }
};
</script>
<style>
.card-header {
  cursor: pointer;
}
</style>
