<template>
  <div>
    <h1>{{ item.machineName }}</h1>
   <!-- <h4>{{ "Machine Status: " + item.status }}</h4>-->
    <div>{{ item.machineDescription }}</div>
    <div>
      {{
        "Manufacturer: " + item.manufacturer + "  |  Model: " + item.model
      }}
    </div>
    <div>
      {{
        "Model: " + item.serial + "  |  MacAddress: " + item.mac
      }}
    </div>
  </div>
</template>

<script>
export default {
  name: "current-machine",
  props: ["item"]
};
</script>