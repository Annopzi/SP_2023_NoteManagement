<template>
  <div>
    <h1>ทำวันที่เป็นไทย</h1>
    <h1>ใช้ show {{ formattedDateTwo }}</h1>
    <h1>ใช้กับ db {{ date }}</h1>
    <v-col cols="12" sm="6" md="4">
      <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        :return-value.sync="formattedDateTwo"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="formattedDateTwo"
            label="รูปแบบไทย"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          no-title
          scrollable
          format="yyyy-MM-dd"
          locale="th"
        >
          <v-spacer></v-spacer>
          <v-btn text color="primary" @click="menu = false"> Cancel </v-btn>
          <v-btn text color="primary" @click="$refs.menu.save(date)">
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
    <h1>Start {{ dateStart }}</h1>
    <v-col cols="12" sm="6" md="4">
      <v-menu
        ref="menu"
        v-model="menuStart"
        :close-on-content-click="false"
        :return-value.sync="dateStart"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="dateStart"
            label="Picker in menu"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker v-model="dateS" no-title scrollable
          format="yyyy-MM-dd"
          locale="th"
          > </v-date-picker>
      </v-menu>
    </v-col>
    <h1>End{{ dateEnd }}</h1>
    <v-col cols="12" sm="6" md="4">
      <v-menu
        ref="menu"
        v-model="menuEnd"
        :close-on-content-click="false"
        :return-value.sync="dateEnd"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="dateEnd"
            label="Picker in menu"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <!-- ก็แค่นี้ -->
        <v-date-picker v-model="dateE" no-title scrollable :min="dateS"
        format="yyyy-MM-dd"
          locale="th">
        </v-date-picker>
      </v-menu>
    </v-col>
  </div>
</template>

<script>
import moment from "moment";
export default {
  data() {
    return {
      dateStart: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      dateEnd: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      dateS: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10), 
      dateE: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10), 
      formattedDateTwo: new Date(
        Date.now() - new Date().getTimezoneOffset() * 60000
      )
        .toISOString()
        .substr(0, 10),
      menu: false,
      menuStart: false,
      menuEnd: false,
    };
  },
  created() {
    this.formattedDateTwo = moment().add(543, "years").format("DD-MM-YYYY");
    this.dateStart = moment().add(543, "years").format("DD-MM-YYYY");
    this.dateEnd = moment().add(543, "years").format("DD-MM-YYYY");
  },
  updated() {
    const formattedDateTwo = moment(this.date)
      .add(543, "years")
      .format("DD-MM-YYYY");
    this.formattedDateTwo = formattedDateTwo;
    
    const dateStart = moment(this.dateS)
      .add(543, "years")
      .format("DD-MM-YYYY");
      this.dateStart = dateStart;

          const dateEnd = moment(this.dateE)
      .add(543, "years")
      .format("DD-MM-YYYY");
      this.dateEnd = dateEnd;
      
  },
};
</script>

<style scoped>
* {
  font-family: "Lato", sans-serif;
}
</style>