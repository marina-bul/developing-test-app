<template>
  <v-dialog max-width="600px" v-model="dialog">
    <template v-slot:activator="{ on, attrs }">
      <v-btn v-bind="attrs" v-on="on" outlined color="#1A237E">
        <slot></slot>
      </v-btn>
    </template>
    <v-card>
      <v-card-title class="text-h5 indigo lighten-5">{{ title }}</v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-text-field
            v-model="lastname"
            :rules="textRules"
            label="Фамилия"
            required
          ></v-text-field>

          <v-text-field v-model="name" :rules="textRules" label="Имя" required></v-text-field>

          <v-text-field
            v-model="patronymic"
            :rules="textRules"
            label="Отчество"
            required
          ></v-text-field>

          <v-text-field v-model="post" :rules="textRules" label="Должность" required></v-text-field>

          <v-text-field v-model="salary" :rules="salaryRules" label="Оклад" required></v-text-field>

          <v-select
            v-model="select"
            :items="items"
            :rules="[(v) => !!v || 'Выберите значение из списка!']"
            label="Ставка"
            required
          ></v-select>

          <v-text-field v-model="currentDate" type="date"></v-text-field>

          <v-checkbox
            v-model="checkbox"
            :rules="[(v) => !!v || 'Сотрудник должен сдать трудовую книжку!']"
            label="Трудовая книжка сдана"
            required
          ></v-checkbox>

          <v-btn :disabled="!valid" color="success" class="mr-4" @click="submit"> Сохранить </v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "modal-window",
  props: {
    title: {
      type: String,
    },
    employeeData: {
      type: Object,
    },
  },
  data: () => ({
    dialog: false,
    valid: true,
    name: "",
    lastname: "",
    patronymic: "",
    post: "",
    salary: 0,
    select: null,
    items: ["полная", "половина"],
    checkbox: false,
    currentDate: new Date().toLocaleString().substr(0, 10).split(".").reverse().join("-"),
    salaryRules: [
      (v) => !!v || "Пожалуйста, заполните поле!",
      (v) => (v && /^(\d+)$/.test(v)) || "Поле должно содержать только цифры!",
      (v) => (v && v >= 10000) || "Сумма должна быть не менее 10000 руб!",
    ],
    textRules: [
      (v) => !!v || "Пожалуйста, заполните поле!",
      (v) =>
        (v && /^([а-я]+)$/iu.test(v)) || "Поле должно содержать только буквы русского алфавита!",
    ],
  }),
  methods: {
    submit() {
      this.$refs.form.validate();
      const newEmployee = {
        lastname: this.lastname,
        name: this.name,
        patronymic: this.patronymic,
        post: this.post,
        salary: this.salary,
        dateOfEntry: this.currentDate,
        isDocumentsCompleted: this.checkbox,
      };
      if (!this.employeeData) {
        newEmployee.id = Date.now();
        this.$emit("addEmployee", newEmployee);
        this.removeInputValues();
      } else {
        newEmployee.id = this.employeeData.id;
        this.$emit("updateEmployee", newEmployee);
      }
      this.dialog = false;
    },
    removeInputValues() {
      this.name = "";
      this.lastname = "";
      this.patronymic = "";
      this.post = "";
      this.salary = 0;
      this.select = null;
      this.checkbox = false;
    },
  },
  mounted() {
    if (this.employeeData) {
      this.name = this.employeeData.name;
      this.lastname = this.employeeData.lastname;
      this.patronymic = this.employeeData.patronymic;
      this.post = this.employeeData.post;
      this.salary = this.employeeData.salary;
      this.currentDate = this.employeeData.dateOfEntry;
      this.select = null;
      this.checkbox = this.employeeData.isDocumentsCompleted;
    }
  },
};
</script>
