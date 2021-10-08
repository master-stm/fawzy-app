<template>
  <q-btn
    v-for="item in shifts"
    :key="item.id"
    color="primary"
    icon="check"
    label="OK"
    @click="onClick"
  />
</template>

<script>
export default {
  name: "Shifts",
  setup() {
    return {
      shifts: [],
    };
  },
  methods: {
    onClick() {
      console.log(this.shifts);
    },
  },
  async created() {
    let res = await fetch("http://localhost:3000/shifts");
    let data = await res.json();
    this.shifts = data;
  },
};
</script>
