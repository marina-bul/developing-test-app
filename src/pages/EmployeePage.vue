<template>
  <v-card class="mx-auto mt-10" color="#7986CB" dark max-width="600px">
    <v-card-title>
      <span class="text-h5 font-weight-bold">Данные сотрудника</span>
    </v-card-title>

    <v-card-text class="d-flex justify-space-between">
      <div>
        <v-avatar class="profile" color="grey" size="164" tile>
          <v-img
            src="https://static.vecteezy.com/system/resources/previews/003/337/584/original/default-avatar-photo-placeholder-profile-icon-vector.jpg"
          ></v-img>
        </v-avatar>
      </div>
      <v-row>
        <v-col cols="4">
          <v-subheader>Фамилия</v-subheader>
          <v-subheader>Имя</v-subheader>
          <v-subheader>Отчество</v-subheader>
          <v-subheader>Должность</v-subheader>
        </v-col>
        <v-col cols="6">
          <v-text-field
            :value="$route.params.item.lastname"
            :disabled="isDisabled"
            dense
          ></v-text-field>
          <v-text-field
            :value="$route.params.item.name"
            :disabled="isDisabled"
            dense
          ></v-text-field>
          <v-text-field
            :value="$route.params.item.patronymic"
            :disabled="isDisabled"
            dense
          ></v-text-field>
          <v-text-field
            :value="$route.params.item.post"
            :disabled="isDisabled"
            dense
          ></v-text-field>
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    isDisabled: true,
  }),
};
</script>
