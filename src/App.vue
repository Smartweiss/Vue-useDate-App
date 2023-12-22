
<template>
  <div class="app">
    <h1 class="newdate">{{ newdate }}</h1>

    <div>
      <p class="day">
  Day: {{ newDay() }}
  <span v-if="addedDay !== 0" class="newDay">
    {{ addedDay === 1 ? ` (+ ${addedDay} day)` : ` (+ ${addedDay} days)` }}
  </span>
</p>
      <button @click="handleAddedDay">Add Days</button>
    </div>

    <div>
      <p class="month">
        Month: {{ newMonth() }}
        <span class="newMonth">
          {{ addedMonth === 0
            ? null
            : addedMonth === 1
            ? ` (+ ${addedMonth} month)`
            : ` (+ ${addedMonth} months)` }}
        </span>
      </p>
      <button @click="handleAddedMonth">Add Months</button>
    </div>

    <div class="action-btn">
      <button
        @click="setNewDate"
        class="change-btn"
        title="Click to set new date"
      >
        Change The World!
      </button>
      <button @click="handleReset" class="reset-btn">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      addedDay: 0,
      addedMonth: 0,
      newdate: new Date().toString(),
    };
  },
  methods: {
    addDay(numberOfDays, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setDate(newDate.getDate() + numberOfDays);

      return newDate;
    },
    addMonth(numberOfMonths, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setMonth(newDate.getMonth() + numberOfMonths);

      return newDate;
    },
    useDate() {
      return {
        date: this.date,
        addDay: this.addDay,
        addMonth: this.addMonth,
      };
    },
    handleAddedDay() {
      this.addedDay += 1;
    },
    handleAddedMonth() {
      this.addedMonth += 1;
    },
    handleAddedDaysAndMonths() {
      const resultDate = this.addMonth(this.addedMonth, this.addDay(this.addedDay));
      return resultDate.toString();
    },
    newMonth() {
      return this.addMonth(this.addedMonth).getMonth() + 1;
    },
    newDay() {
      return this.addDay(this.addedDay).getDate();
    },
    handleReset() {
      this.newdate = this.date.toString();
      this.addedDay = 0;
      this.addedMonth = 0;
    },
    setNewDate() {
      this.newdate = this.handleAddedDaysAndMonths().toString();
    },
  },
};
</script>

<style scoped>
/* Your styles from style.css go here */
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  /* 1rem = 10px(62.5%) */
  font-size: 62.5%;
}

body {
  min-width: 32rem;
  min-height: 100vh;
  font-size: 1.6rem;
  display: flex;
  place-items: center;
  justify-content: center;
  align-items: center;
}

h1 {
  font-size: 2.4rem;
  line-height: 1.1;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6rem 1.2rem;
  margin-top: 0.4rem;
  font-size: 1.2rem;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}

button:hover {
  border-color: #646cff;
}

button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

#app {
  padding: 2rem;
  text-align: center;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
 
}

.action-btn {
  display: flex;
  gap: 2rem;
}


.action-btn > button {
  width: 14rem;
  height: 3.2rem;
}

.change-btn {
  background-color: green;
}

.reset-btn {
  background-color: red;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }

  button {
    background-color: #f9f9f9;
  }
}
.newdate{
color: white;
}
.newDay{
  color:green;
  font-size:15px;
}
.day{
  color: red;
  font-size: 15px;
}
.month{
  color: red;
  font-size: 15px;
}
.newMonth{
  color:green;
  font-size:15px;
}
</style>