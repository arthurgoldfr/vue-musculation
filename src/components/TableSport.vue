<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table ref="refName" :headers="headers" :items="exercices" :items-per-page="5" :search="search" @current-items="createGraph">
      <template v-slot:item.FocusRegions="{ item }">
        <v-chip v-for="el in item.FocusRegions" :key="el" :color="getColor(el)" dark>{{ el }}</v-chip>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
// import { DataFrame } from 'pandas-js';
export default {
  name: "TableSport",
  data() {
    return {
      search: "",
      focusRegions: {},
      headers: [
        {
          text: "Exercices",
          align: "start",
          value: "Exercise"
        },
        { text: "Focus Regions", value: "FocusRegions" },
        { text: "Series", value: "Series" },
        { text: "Weight (kg)", value: "Weight" },
        { text: "Repetitions", value: "Reps" },
        { text: "Rising Time (sec)", value: "RestingTime" },
        { text: "Date", value: "Date" }
      ],
      exercices: [
        {
          Exercise: "Dips",
          FocusRegions: ["Chest", "Shoulders", "Triceps"],
          Series: 4.0,
          Weight: 0.0,
          Reps: 14.0,
          RestingTime: 150.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 3.0,
          Weight: 50.0,
          Reps: 7.0,
          RestingTime: 240.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Tilted press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 22.0,
          Reps: 6.0,
          RestingTime: 200.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Splits squats dumbels",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 2.0,
          Weight: 18.0,
          Reps: 8.0,
          RestingTime: 150.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Lateral elevation dumbels",
          FocusRegions: ["Forearm", "Shoulders", "Trapezius"],
          Series: 3.0,
          Weight: 8.0,
          Reps: null,
          RestingTime: 100.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Curl dumbels",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 14.0,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Sep 14, 2020"
        },
        {
          Exercise: "Pull ups",
          FocusRegions: ["Back", "Shoulders", "Trapezius"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 7.0,
          RestingTime: 200.0,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 57.5,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 7.0,
          RestingTime: 200.0,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 35.0,
          Reps: 6.0,
          RestingTime: 200.0,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Chest pull",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 23.0,
          Reps: 8.0,
          RestingTime: null,
          Date: "Sep 16, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 60.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 57.5,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 3.0,
          Weight: 25.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 27.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Hyperextensions with plate",
          FocusRegions: ["Lumbar"],
          Series: 2.0,
          Weight: 15.0,
          Reps: 10.0,
          RestingTime: 60.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Legs elevation",
          FocusRegions: ["Abs", "Lumbar"],
          Series: 3.0,
          Weight: 0.0,
          Reps: 10.0,
          RestingTime: 60.0,
          Date: "Sep 21, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 62.5,
          Reps: 5.0,
          RestingTime: 210.0,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Glutes", "Legs", "Lumbar", "Trapezius"],
          Series: 2.0,
          Weight: 70.0,
          Reps: 5.0,
          RestingTime: 210.0,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 37.5,
          Reps: 5.0,
          RestingTime: 210.0,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 50.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Incline chest dumbells",
          FocusRegions: ["Chest", "Shoulders", "Triceps"],
          Series: 3.0,
          Weight: 22.0,
          Reps: 8.0,
          RestingTime: null,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Legs elevation",
          FocusRegions: ["Abs", "Lumbar"],
          Series: 3.0,
          Weight: 0.0,
          Reps: 10.0,
          RestingTime: null,
          Date: "Sep 23, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 65.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 57.5,
          Reps: 5.0,
          RestingTime: 240.0,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 3.0,
          Weight: 27.5,
          Reps: 8.0,
          RestingTime: null,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 27.0,
          Reps: 8.0,
          RestingTime: null,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 11.25,
          Reps: 8.0,
          RestingTime: null,
          Date: "Sep 25, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Glutes", "Legs", "Lumbar", "Soleus"],
          Series: 1.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 210.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 40.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 50.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Sep 28, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 60.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 3.0,
          Weight: 60.0,
          Reps: 8.0,
          RestingTime: 180.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 11.25,
          Reps: 8.0,
          RestingTime: 180.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 32.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Hyperextensions with plate",
          FocusRegions: ["Lumbar"],
          Series: 2.0,
          Weight: 20.0,
          Reps: 10.0,
          RestingTime: 90.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Legs elevation",
          FocusRegions: ["Abs", "Lumbar"],
          Series: 3.0,
          Weight: 0.0,
          Reps: 10.0,
          RestingTime: 90.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Dips",
          FocusRegions: ["Chest", "Shoulders", "Triceps"],
          Series: 3.0,
          Weight: 0.0,
          Reps: 10.0,
          RestingTime: 90.0,
          Date: "Sep 30, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Glutes", "Legs", "Lumbar", "Soleus"],
          Series: 1.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 210.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 37.5,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 52.5,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Legs elevation",
          FocusRegions: ["Abs", "Lumbar"],
          Series: null,
          Weight: null,
          Reps: null,
          RestingTime: null,
          Date: "Oct 2, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 80.0,
          Reps: 10.0,
          RestingTime: 240.0,
          Date: "Oct 5, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 60.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 5, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 6.0,
          RestingTime: 150.0,
          Date: "Oct 5, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Trapezius"],
          Series: 3.0,
          Weight: 70.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Oct 5, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 77.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Glutes", "Legs", "Lumbar", "Soleus"],
          Series: 1.0,
          Weight: 85.0,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 40.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 70.0,
          Reps: 6.0,
          RestingTime: 180.0,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 55.0,
          Reps: 8.0,
          RestingTime: 180.0,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 10.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Oct 7, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 62.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 75.0,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Trapezius"],
          Series: 3.0,
          Weight: 60.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 32.0,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 11.25,
          Reps: 8.0,
          RestingTime: 90.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Hyperextensions with plate",
          FocusRegions: ["Lumbar"],
          Series: 2.0,
          Weight: 22.5,
          Reps: 10.0,
          RestingTime: 90.0,
          Date: "Oct 9, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 12, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Glutes", "Legs", "Lumbar", "Soleus"],
          Series: 1.0,
          Weight: 90.0,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 12, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 40.0,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Oct 12, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 77.5,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Oct 12, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 12.5,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 12, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 62.5,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 77.5,
          Reps: 5.0,
          RestingTime: 150.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 82.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Trapezius"],
          Series: 3.0,
          Weight: 60.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 32.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 11.25,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Hyperextensions with plate",
          FocusRegions: ["Lumbar"],
          Series: 2.0,
          Weight: 25.0,
          Reps: 10.0,
          RestingTime: 120.0,
          Date: "Oct 14, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 57.5,
          Reps: 8.0,
          RestingTime: 150.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: 55.0,
          Reps: 10.0,
          RestingTime: null,
          Date: "Oct 21, 2020"
        },
        {
          Exercise: "Close grip bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 3.0,
          Weight: null,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 26, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: null,
          Series: 1.0,
          Weight: 100.0,
          Reps: 5.0,
          RestingTime: 0.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 42.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 80.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 12.5,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 84.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 16, 2020"
        },
        {
          Exercise: "Hyperextensions with plate",
          FocusRegions: ["Lumbar"],
          Series: 2.0,
          Weight: null,
          Reps: 10.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Curl bar EZ",
          FocusRegions: ["Biceps", "Forearm"],
          Series: 3.0,
          Weight: 12.5,
          Reps: 8.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Triceps extension",
          FocusRegions: ["Triceps"],
          Series: 3.0,
          Weight: 32.0,
          Reps: 8.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Trapezius"],
          Series: 3.0,
          Weight: 65.0,
          Reps: 8.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Barbell Shrugs",
          FocusRegions: ["Trapezius"],
          Series: 3.0,
          Weight: 65.0,
          Reps: 8.0,
          RestingTime: 120.0,
          Date: "Oct 23, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 83.5,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 77.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 78.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 21, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Lumbar", "Shoulders"],
          Series: 5.0,
          Weight: 77.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 23, 2020"
        },
        {
          Exercise: "Rowing",
          FocusRegions: ["Back", "Legs", "Shoulders"],
          Series: 5.0,
          Weight: 79.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 26, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 64.0,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Bench press",
          FocusRegions: ["Chest", "Triceps"],
          Series: 5.0,
          Weight: 61.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 23, 2020"
        },
        {
          Exercise: "Abs crunch",
          FocusRegions: ["Abs"],
          Series: 2.0,
          Weight: 50.0,
          Reps: 10.0,
          RestingTime: null,
          Date: "Oct 19, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 82.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 21, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 85.0,
          Reps: 5.0,
          RestingTime: 200.0,
          Date: "Oct 23, 2020"
        },
        {
          Exercise: "Squats bar",
          FocusRegions: ["Glutes", "Legs", "Soleus"],
          Series: 5.0,
          Weight: 86.0,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 26, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Glutes"],
          Series: 1.0,
          Weight: 100.0,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 21, 2020"
        },
        {
          Exercise: "Deadlift",
          FocusRegions: ["Back", "Lumbar"],
          Series: 1.0,
          Weight: 105.0,
          Reps: 5.0,
          RestingTime: 0.0,
          Date: "Oct 26, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders", "Trapezius"],
          Series: 5.0,
          Weight: 41.5,
          Reps: 5.0,
          RestingTime: null,
          Date: "Oct 21, 2020"
        },
        {
          Exercise: "Standing press",
          FocusRegions: ["Shoulders"],
          Series: 5.0,
          Weight: 42.5,
          Reps: 5.0,
          RestingTime: 180.0,
          Date: "Oct 26, 2020"
        }
      ]
    };
  },
  props: ["region_colors"],
  methods: {
    getColor(el) {
      console.log(this.region_colors)
      if (typeof el === "string") {
        for (const name of Object.keys(this.region_colors)) {
          if (el.includes(name)) 
          {
            return this.region_colors[name];
          }
        }
      }
    },
    createGraph() {
      let items = this.$refs.refName.$children[0].filteredItems;
      Object.keys(this.region_colors).forEach(name => {
        this.focusRegions[name] = 0;
        items.forEach(exercise => {
          if (exercise.FocusRegions != undefined) {
            if (exercise.FocusRegions.includes(name)){
              this.focusRegions[name] ++;
              //console.log(this.FocusRegions);
            }
          }
        })
      })
    console.log("ok")
    console.log(this.FocusRegions);
    let value = this.focusRegions;
    this.$emit('changed', value);
    }
  },
  mounted () {
    this.createGraph()
  }
};
</script>
