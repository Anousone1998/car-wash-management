<template>
  <div >
    <h2 class="mt-3">Manage Employees</h2>
    <br>
    <employees/>
  </div>
</template>
<script>
import employees from '@/components/tables/employees'
  export default {
    components: {
     employees
    },
  }
</script>
