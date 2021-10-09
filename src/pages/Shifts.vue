<template>
  <q-list bordered padding>
    <q-item-label header>Admins</q-item-label>

    <q-separator spaced />
    <q-item>
      <q-item-section>
        <q-item-section><strong>Staff / Role</strong></q-item-section>
      </q-item-section>
      <q-item-section><strong>From</strong></q-item-section>
      <q-item-section>
        <q-item-label><strong>To</strong></q-item-label>
      </q-item-section>
      <q-item-label><strong>Working Hours</strong></q-item-label>
    </q-item>
    <div v-for="shift in shifts" :key="shift.id">
      <q-item v-if="shift.staff.role === 'Admin'">
        <q-item-section>
          <q-item-section>{{ shift.staff.name }}</q-item-section>
          <q-item-section>{{ shift.staff.role }}</q-item-section>
        </q-item-section>
        <q-item-section>{{ shift.startTime }}</q-item-section>
        <q-item-section>
          <q-item-label>{{ shift.endTime }}</q-item-label>
        </q-item-section>
        <q-item-label>{{ shift.workingHours }}</q-item-label>
      </q-item>
    </div>

    <q-separator spaced />
    <q-item-label header>Nurses</q-item-label>
    <q-separator spaced />
    <q-item>
      <q-item-section>
        <q-item-section><strong>Staff / Role</strong></q-item-section>
      </q-item-section>
      <q-item-section><strong>From</strong></q-item-section>
      <q-item-section>
        <q-item-label><strong>To</strong></q-item-label>
      </q-item-section>
      <q-item-label><strong>Working Hours</strong></q-item-label>
    </q-item>
    <div v-for="shift in shifts" :key="shift.id">
      <q-item v-if="shift.staff.role === 'Nurse'">
        <q-item-section>
          <q-item-section>{{ shift.staff.name }}</q-item-section>
          <q-item-section>{{ shift.staff.role }}</q-item-section>
        </q-item-section>
        <q-item-section>{{ shift.startTime }}</q-item-section>
        <q-item-section>
          <q-item-label>{{ shift.endTime }}</q-item-label>
        </q-item-section>
        <q-item-label>{{ shift.workingHours }}</q-item-label>
      </q-item>
    </div>
  </q-list>
</template>

<script>
export default {
  name: "Shifts",
  data() {
    return {
      shifts: [],
    };
  },
  methods: {},
  async mounted() {
    let res = await fetch("http://localhost:3000/shifts");
    let data = await res.json();
    this.shifts = data;
  },
};
</script>
