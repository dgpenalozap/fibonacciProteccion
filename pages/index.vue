<script>
import { onMounted } from "vue";
import { useDisplay } from "vuetify";

export default {
  setup() {
    const { mobile } = useDisplay();

    onMounted(() => {
      console.log(mobile.value); // false
    });
  },
  data() {
    return {
      time: "",
      serief: "",
      x: "",
      y: "",
      z: "",
      hora: ""
    };
  },
  mounted() {
    this.updateTime();
    setInterval(() => {
      this.updateTime();
    }, 1000);
  },
  methods: {
    updateTime() {
      const date = new Date();
      const hours = date.getHours();
      const minutes = date.getMinutes();
      const minutesString = minutes.toString().padStart(2, "0");
      const firstDigit = parseInt(minutesString[0]);
      const secondDigit = parseInt(minutesString[1]);
      const seconds = date.getSeconds();
      this.time = `${hours}:${firstDigit}${secondDigit}:${seconds}`;
    },
    showfibonacci() {
      const date = new Date();

      const options = {
        weekday: "long",
        year: "numeric",
        month: "long",
        day: "numeric",
      };
      const dateString = date.toLocaleDateString("es-ES", options);
      console.log("Fecha:", dateString);

      const timeString = date.toLocaleTimeString("es-ES");
      console.log("Hora:", timeString);

      const hours = date.getHours();
      const minutes = date.getMinutes();
      const seconds = date.getSeconds();

      console.log("Horas:", hours);
      console.log("Minutos:", minutes);
      console.log("Segundos:", seconds);

      const minutesString = minutes.toString().padStart(2, "0");
      const firstDigit = parseInt(minutesString[0]);
      const secondDigit = parseInt(minutesString[1]);

      console.log("Primer dígito de los minutos:", firstDigit);
      console.log("Segundo dígito de los minutos:", secondDigit);
      this.hora = `${hours}:${firstDigit}${secondDigit}:${seconds}`;

      function fibonacci(x, y, z) {
        let result = [x, y];
        for (let i = 2; i < z; i++) {
          result.push(result[i - 2] + result[i - 1]);
        }
        console.log(result.reverse().join(", "));
        return result;
      }
      
      let digitSeconds;

      if (seconds < 10) {
        const secondsString = seconds.toString().padStart(2, "0");
        digitSeconds = parseInt(secondsString[1]);
      } else {
        digitSeconds = seconds;
      }
      this.x = firstDigit 
      this.y = secondDigit
      this.z = digitSeconds;
      this.serief = fibonacci(firstDigit, secondDigit, digitSeconds);
    },
    cleanshow() {
      this.serief = "";
    },
  },
};
</script>
<template>
  <div class="mini-spacer">
    <v-container >
    <div class="center-div">
      <h3>La hora actual es </h3>
    </div>
    <div class="center-div">
      <h3>{{ time }}</h3>
    </div>
    <div style="height: 30px"></div>
    <div class="center-div">
      <v-btn @click="showfibonacci()" color="secondary">
        Mostrar FIbonacci</v-btn
      >
    </div>
    <div style="height: 10px"></div>
    <div class="center-div">
      <v-btn @click="cleanshow()" color="primary"> Limpiar</v-btn>
    </div>
    <div style="height: 30px"></div>
    <div class="center-div">
      <p> La serie Fibonacci es</p>
    </div>
    <div class="center-div">
      <p> Hora: {{ hora }}</p>
    </div>
    <div class="center-div">
      <p> Semillas x={{ x }}, y={{ y }} y N muestras z={{ z }}</p>
    </div>
    <div style="height: 30px"></div>
    <div class="center-div">
      <p>{{ serief }}</p>
    </div>
  </v-container>
  </div>
</template>
<style>
.center-div {
  display: flex;
  justify-content: center;
}
.mini-spacer {
  padding-top: 100px;
}
</style>
