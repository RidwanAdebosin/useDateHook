<template>
  <h1>Date: {{ currentDate }}</h1>
  <h1>Day: {{ day }}</h1>
  <h1>Month: {{ month }}</h1>

  <form @submit.prevent="AddDate">
    <div class="container">
      <div>
        <label for="day"> Day: </label>
        <input
          type="number"
          name="day"
          placeholder="Enter day..."
          v-model="dateobj.day"
        />
      </div>

      <div>
        <label for="month"> Month: </label>
        <input
          type="number"
          name="month"
          id=""
          placeholder="Enter month..."
          v-model="dateobj.month"
        />
      </div>
      <div>
        <label for="year"> Year: </label>
        <input
          type="number"
          name="year"
          id=""
          placeholder="Enter year..."
          v-model="dateobj.year"
        />
      </div>

      <button>Get Day</button>
    </div>
  </form>

  <p>{{ customDate }}</p>
</template>

<script>
import { onMounted, ref } from "vue";
import useDate from "../components/UseDate";

export default {
  setup() {
    const { date, getDay, getMonth, createCustomDate } = useDate();

    let day = ref(null);
    let month = ref(null);
    let currentDate = ref(null);
    let customDate = ref(null);
    let dateobj = ref({
      day: null,
      month: null,
      year: null,
    });

    onMounted(() => {
      currentDate.value = date.toString();
      day.value = getDay();
      month.value = getMonth();
    });

    function AddDate() {
      customDate.value = createCustomDate(
        dateobj.value.year,
        dateobj.value.month,
        dateobj.value.day
      );
    }

    return { currentDate, day, month, customDate, AddDate, dateobj };
  },
};
</script>

<style>
form {
  max-width: 500px;
  background-color: #ccc;
  border-radius: 10px;
  margin: 0 auto;
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.3);
  padding: 10px;
}

.container {
  display: flex;
  text-align: center;
  justify-content: center;
  flex-direction: column;
  gap: 10px;
}

form input {
  padding: 10px;
  width: 70%;
  border-radius: 6px;
  border: none;
}

form label {
  display: block;
  font-size: 20px;
  margin-block-end: 5px;
}

button {
  display: flex;
  margin: 0 auto;
  padding: 10px 25px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
}

button:hover {
  font-weight: 700;
  background-color: transparent;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3);
  transition: all 300ms ease-in-out;
}
</style>
