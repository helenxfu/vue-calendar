<template>
  <div class="container">
    <div class="head">
      <button @click="previous">&#8249;</button>
      <h2>{{months[viewingMonth]}} {{viewingYear}}</h2>
      <button @click="next">&#8250;</button>
    </div>
    <div class="gridClass weekContainer">
      <div v-for="weekName in week" :key="weekName" class="weekLabel">{{weekName}}</div>
    </div>
    <div class="gridClass boxContainer">
      <div v-for="blank in blankBox" :key="'blank'+blank"></div>
      <div v-for="day in daysInMonth" :key="day" class="box" :class="classToday(day)">{{day}}</div>
    </div>
    <div class="foot">
      <form>
        <label>Select Year and Month:</label>
        <select v-model="viewingYear" name="year">
          <option v-for="option in options" :key="option" :value="option">{{option}}</option>
        </select>
        <select v-model="viewingMonth" name="month">
          <option v-for="(month, index) in months" :key="month" :value="index">{{month}}</option>
        </select>
      </form>
      <button @click="reset">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calendar",
  data() {
    return {
      today: new Date(),
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ],
      monthsShort: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ],
      week: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      options: [],
      viewingMonth: 0,
      viewingYear: 0,
      currentMonth: 0,
      currentYear: 0,
      currentDate: 0
    };
  },
  created: function() {
    this.viewingMonth = this.currentMonth = this.today.getMonth();
    this.viewingYear = this.currentYear = this.today.getFullYear();
    this.currentDate = this.today.getDate();
    let date = this.currentYear - 3;
    for (let i = 0; i < 6; i++) {
      this.options.push(date + i);
    }
  },
  computed: {
    daysInMonth() {
      //how many days in month
      return 32 - new Date(this.viewingYear, this.viewingMonth, 32).getDate();
    },
    blankBox() {
      let firstDay = new Date(this.viewingYear, this.viewingMonth).getDay();
      return firstDay;
    }
  },
  methods: {
    next() {
      this.viewingYear =
        this.viewingMonth === 11 ? this.viewingYear + 1 : this.viewingYear;
      this.viewingMonth = (this.viewingMonth + 1) % 12;
    },
    previous() {
      this.viewingYear =
        this.viewingMonth === 0 ? this.viewingYear - 1 : this.viewingYear;
      this.viewingMonth = this.viewingMonth === 0 ? 11 : this.viewingMonth - 1;
    },
    reset() {
      this.viewingYear = this.currentYear;
      this.viewingMonth = this.currentMonth;
    },
    classToday(day) {
      if (
        this.viewingYear === this.currentYear &&
        this.viewingMonth === this.currentMonth &&
        day === this.currentDate
      ) {
        return "today";
      }
      return "";
    }
  }
};
</script>

<style scoped>
.container {
  min-width: 320px;
  max-width: 600px;
  margin: auto;
  border: 2px solid rgb(214, 177, 53);
  border-radius: 5px;
}
.head {
  background-color: rgb(100, 112, 108);
  color: rgb(240, 248, 255);
  text-align: center;
  padding: 5px;
  display: flex;
  justify-content: center;
}
.head > button {
  background-color: transparent;
  color: white;
  padding: 5px 30px;
}
.gridClass {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
}
.weekContainer {
  background-color: rgb(124, 136, 126);
  font-weight: bold;
  color: rgb(235, 234, 229);
}
.weekLabel {
  padding: 5px 0;
  font-size: 18px;
  border: 0.5px dashed rgba(245, 147, 147, 0.3);
}
.weekLabel:nth-child(1) {
  background-color: rgb(147, 83, 71);
}
.weekLabel:nth-child(7) {
  background-color: rgb(69, 69, 121);
}
.boxContainer {
  background-color: rgb(163, 153, 118);
  background-image: url("https://helenxfu.github.io/assets/cats/starcloudLogo.png");
  background-repeat: no-repeat;
  background-position: center;
}
.box {
  border: 0.5px dashed rgba(138, 108, 108, 0.3);
  height: 80px;
  background-color: rgba(255, 242, 211, 0.7);
  color: rgb(61, 56, 5);
  padding-top: 5px;
  transition-duration: 0.5s;
  transition-property: background-color, border-radius, transform;
}
.box:hover {
  background-color: rgba(240, 239, 232, 0.8);
  border-radius: 10px;
  transform: scale(1.3);
  font-size: 18px;
}
.box:nth-child(7n + 1) {
  background-color: rgba(230, 208, 200, 0.7);
  color: rgb(58, 14, 23);
}
.box:nth-child(7n) {
  background-color: rgba(219, 226, 221, 0.7);
  color: rgb(54, 54, 82);
}
.today {
  background-color: rgba(254, 255, 199, 0.7) !important;
  color: rgb(112, 124, 4) !important;
}
.foot {
  background-color: rgb(114, 104, 112);
  color: rgb(211, 210, 205);
  padding: 10px;
  display: flex;
  justify-content: center;
}
label {
  font-size: 16px;
}
</style>