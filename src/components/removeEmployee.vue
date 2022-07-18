<template>
  <v-dialog v-model="dialog" width="500">
    <template v-slot:activator="{ on, attrs }">
      <v-btn v-bind="attrs" v-on="on" icon color="indigo darken-3">
        <v-icon>mdi-trash-can </v-icon>
      </v-btn>
    </template>

    <v-card>
      <v-card-title class="text-h5 indigo lighten-4"> Удаление сотрудника </v-card-title>

      <v-card-text class="mt-5"> Вы уверены, что хотите удалить этого сотрудника? </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" text @click="acceptRemoving"> Да </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "remove-employee",
  props: {
    personId: {
      type: Number,
      required: true,
    },
  },
  data: () => ({
    dialog: false,
  }),
  methods: {
    acceptRemoving() {
      this.dialog = false;
      this.$emit("remove", this.personId);
    },
  },
};
</script>
