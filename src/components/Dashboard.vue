<template>
  <v-main>
    <h1>Dashboard</h1>
    <!-- v-row создержит 12 колонок автоматически -->
    <v-row id="below-the fold" v-intersect="showMoreContent">
      <v-col v-for="item in 4" :key="item" xl="3" lg="4" md="6" xs="12">
        <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="5"
          class="elevation-1"
          @click:row="selectRow"
        ></v-data-table
      ></v-col>
    </v-row>
    <!-- если мы в v-row создаем две v-col то оно автоматически делит на две колонки с шириной 50 % -->
    <v-row>
      <v-col>
        <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="5"
          class="elevation-1"
          @click:row="selectRow"
        ></v-data-table
      ></v-col>
      <v-col>
        <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="5"
          class="elevation-1"
          @click:row="selectRow"
        ></v-data-table>
      </v-col>
    </v-row>
    <!-- создаем две колонки. Одна из них имеет ширину 8 колонок а вторая автоматом занимает остаток то есть 4 -->
    <v-row v-if="loadNewContent" class="loadNewContent">
      <v-col cols="8">
        <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="5"
          class="elevation-1"
          @click:row="selectRow"
        ></v-data-table
      ></v-col>
      <v-col>
        <v-data-table
          :headers="headers"
          :items="desserts"
          :items-per-page="5"
          class="elevation-1"
          @click:row="selectRow"
        ></v-data-table>
      </v-col>
    </v-row>
    <v-data-table
      :headers="headers"
      :items="desserts"
      :items-per-page="5"
      class="elevation-1"
      @click:row="selectRow"
    ></v-data-table>
    <!-- //
    используем краткую форму написания $vuetify.breakpoint и с помощью нее управляем компонентами
    Conditionals
      xsOnly: boolean
      smOnly: boolean
      smAndDown: boolean
      smAndUp: boolean
      mdOnly: boolean
      mdAndDown: boolean
      mdAndUp: boolean
      lgOnly: boolean
      lgAndDown: boolean
      lgAndUp: boolean
      xlOnly: boolean
  -->
    <v-snackbar v-model="snackbar" :left="$vuetify.breakpoint.smAndUp">
      <v-btn color="pink" text  @click="snackbar = false">
        You have selected {{ currentItem }}
      </v-btn>
    </v-snackbar>
  </v-main>
</template>

<script>
export default {
  data() {
    return {
      loadNewContent: false,
      isIntersecting: false,
      currentItem: "",
      snackbar: false,
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%",
        },
      ],
    };
  },
  methods: {
    selectRow(event) {
      (this.snackbar = true), (this.currentItem = event.name);
    },
    showMoreContent(entries){
      console.log(entries[0].isIntersecting)
      this.loadNewContent = entries[0].isIntersecting
    }
  },
};
</script>
<!-- BreakPoints: https://vuetifyjs.com/en/features/breakpoints/  -->
<!-- Это клевая тема при скролировании у нас появляются и исчещают компоненты
  https://vuetifyjs.com/en/directives/intersect/
  https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry
 -->