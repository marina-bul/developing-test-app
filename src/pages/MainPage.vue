<template>
  <v-container fluid>
    <modal-window :title="modalTitle" @addEmployee="addEmployee"> Добавить </modal-window>
    <employee-list
      :staff="staff"
      :headers="tableHeaders"
      @remove="removeEmployee"
      @updateData="updateEmployee"
    />
  </v-container>
</template>

<script>
import ModalWindow from "../components/ModalWindow.vue";
import EmployeeList from "../components/EmployeeList.vue";
export default {
  name: "main-page",
  components: {
    ModalWindow,
    EmployeeList,
  },
  data: () => ({
    modalTitle: "Добавить сотрудника",
    tableHeaders: [
      { text: "Фамилия", value: "lastname", sortable: true },
      { text: "Имя", value: "name", sortable: true },
      { text: "Отчество", value: "patronymic", sortable: false },
      { text: "Должность", value: "post", sortable: false },
      { text: "", value: "actions", sortable: false },
    ],
    staff: [
      {
        lastname: "Лаптев",
        name: "Егор",
        patronymic: "Михайлович",
        post: "инженер",
        salary: 50000,
        dateOfEntry: "2019-06-27",
        isDocumentsCompleted: true,
        id: 1,
      },

      {
        lastname: "Соколова",
        name: "Людмила",
        patronymic: "Борисовна",
        post: "бухгалтер",
        salary: 40000,
        dateOfEntry: "2006-04-30",
        isDocumentsCompleted: true,
        id: 2,
      },

      {
        lastname: "Тарасова",
        name: "Ксения",
        patronymic: "Ивановна",
        post: "секретарь",
        salary: 20000,
        dateOfEntry: "2018-08-13",
        isDocumentsCompleted: false,
        id: 3,
      },

      {
        lastname: "Привезенцев",
        name: "Фёдор",
        patronymic: "Николаевич",
        post: "охранник",
        salary: 20000,
        dateOfEntry: "2020-01-15",
        isDocumentsCompleted: true,
        id: 4,
      },
    ],
  }),
  methods: {
    updateLocalStorage() {
      let parsedData = JSON.stringify(this.staff);
      localStorage.setItem("staff", parsedData);
    },
    addEmployee(employee) {
      this.staff.push(employee);
      this.updateLocalStorage();
    },
    updateEmployee(employee) {
      this.staff = this.staff.filter((item) => item.id != employee.id);
      this.staff.push(employee);
      this.updateLocalStorage();
    },
    removeEmployee(personId) {
      this.staff = this.staff.filter((item) => item.id != personId);
      this.updateLocalStorage();
    },
  },
  mounted() {
    if (localStorage.getItem("staff")) {
      try {
        this.staff = JSON.parse(localStorage.getItem("staff"));
      } catch (e) {
        localStorage.removeItem("staff");
      }
    } else {
      this.updateLocalStorage();
    }
  },
};
</script>
