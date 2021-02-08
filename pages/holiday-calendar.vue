<template>
  <v-row>
    <v-col>
      オリジナルカレンダー
      <v-date-picker v-model="selectedDate" readonly :events="holidays" event-color="red" />
    </v-col>
    <v-col>
      休日を選択して反映する
      <v-date-picker v-model="holidays" multiple />
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      selectedDate: null,
      holidays: null
    }
  }
}
</script>
