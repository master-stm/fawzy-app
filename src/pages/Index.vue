<template>
  <q-page class="flex flex-center">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
      <q-select
        v-model="name"
        :options="staff"
        option-label="name"
        label="Name"
        :hint="name ? 'Role: ' + name.role : ''"
      />

      <input type="datetime-local" v-model="startTime" /><br />
      <input type="datetime-local" v-model="endTime" />

      <div>
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn
          label="Reset"
          type="reset"
          color="primary"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import moment from "moment";
export default defineComponent({
  name: "add staff",
  data() {
    return {
      name: null,
      startTime: null,
      endTime: null,
      staff: [
        {
          name: "Fawzy",
          role: "Admin",
        },
        {
          name: "Aziz",
          role: "Admin",
        },
        {
          name: "Salem",
          role: "Admin",
        },
        {
          name: "Mahmoud",
          role: "Admin",
        },
        {
          name: "Dina",
          role: "Nurse",
        },
        {
          name: "Haydi",
          role: "Nurse",
        },
      ],
    };
  },
  methods: {
    onSubmit() {
      var startTime = this.startTime.split("T").join(" ");
      var endTime = this.endTime.split("T").join(" ");

      let workingHours = moment
        .utc(
          moment(endTime, "YYYY/MM/DD HH:mm").diff(
            moment(startTime, "YYYY/MM/DD HH:mm")
          )
        )
        .format("HH:mm:ss");
      fetch("http://localhost:3000/shifts", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: this.name,
          startTime,
          endTime,
          workingHours,
        }),
      }).then(() => this.onReset());
    },

    onReset() {
      this.name = null;
      this.startTime = null;
      this.endTime = false;
    },
  },
});
</script>
