<!-- eslint-disable vue/valid-v-slot -->
<template>
  <v-card class="mt-5">
    <v-card-title>
      Список сотрудников
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Поиск..."
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="staff"
      :items-per-page="5"
      :custom-sort="customSort"
      :search="search"
      @click:row="goToPersonPage"
      class="elevation-1"
    >
      <template v-slot:item.actions="{ item }">
        <modal-window :title="modalTitle" :employeeData="item" @updateEmployee="update">
          <v-icon>mdi-account-edit </v-icon>
        </modal-window>
        <remove-employee :personId="item.id" @remove="remove" />
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
import ModalWindow from "./ModalWindow.vue";
import removeEmployee from "./removeEmployee.vue";
export default {
  components: { removeEmployee, ModalWindow },
  name: "employee-list",
  props: {
    headers: {
      type: Array,
      required: true,
    },
    staff: {
      type: Array,
      required: true,
    },
  },
  data: () => ({
    modalTitle: "Редактировать",
    search: "",
  }),
  methods: {
    customSort(items, index, isDesc) {
      items.sort((item1, item2) => {
        if (isDesc != "false") {
          return item1[index] < item2[index] ? -1 : 1;
        } else {
          return item2[index] < item1[index] ? -1 : 1;
        }
      });
      return items;
    },
    update(employee) {
      this.$emit("updateData", employee);
    },
    remove(personId) {
      this.$emit("remove", personId);
    },
    goToPersonPage(item) {
      this.$router.push({ name: "EmployeePage", params: { id: item.id, item: item } });
    },
  },
};
</script>
