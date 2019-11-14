<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div
        class="list-group-item d-flex align-items-start"
        v-for="item in machines"
        :key="item.machIndex"
      >
        <button class="mr-2 btn btn-sm btn-danger" @click="$emit('remove', item)">
          <font-awesome-icon icon="trash"/>
        </button>
        <div class="w-100">
          <div class="d-flex justify-content-between">
             <div @click="$emit('handlePick', item)"> <!--emit starts an event in the parent component-->
            <small
              class="text-primary"
              contenteditable="contenteditable"
              @blur="$emit('edit', item.machId, 'machineName', $event.target.innerText)"
            >{{item.machineName}}</small>
            <small class="float-right">{{formattedDate(item.machDate)}}</small>
            <small class="owner-name">
            <small class="font-weight-bold text-primary mr-1">Manufacturer:</small>
            <small
              contenteditable="contenteditable"
              @blur="$emit('edit', item.machId, 'manufacturer', $event.target.innerText)"
            >{{item.manufacturer}}</small>
          </small>
          <small
            contenteditable="contenteditable"
            @blur="$emit('edit', item.machId, 'machineDescription', $event.target.innerText)"
          >{{item.machineDescription}}</small>
          </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import moment from "moment";
export default {
  name: "MachineList",
  props: ["machines"],
  components: {
    FontAwesomeIcon
  },
  methods: {
    formattedDate: function(date) {
      return moment(new Date(date)).format("MM-DD-YY, h:mm a");
    }
  }
};
</script>

