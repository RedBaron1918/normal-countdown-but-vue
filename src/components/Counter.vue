<template>
  <section
    class="text-3xl flex justify-center content-center flex-col mx-auto text-center"
  >
    Timer
  </section>
  <section class="flex text-6xl justify-center content-center">
    <div class="days mr-2 relative">
      {{ Days }}
      <div class="label text-sm absolute bottom-0">Days</div>
    </div>
    <span class="leading-snug">:</span>

    <div class="hours mr-2 relative">
      {{ Hours }}
      <div class="label text-sm absolute bottom-0">Hours</div>
    </div>
    <span class="leading-snug">:</span>

    <div class="minutes mr-2 relative">
      {{ Minutes }}
      <div class="label text-sm absolute bottom-0">Minutes</div>
    </div>
    <span class="leading-snug">:</span>

    <div class="seconds mr-2 relative">
      {{ Seconds }}
      <div class="label text-sm absolute bottom-0">Seconds</div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      Days: 0,
      Hours: 0,
      Minutes: 0,
      Seconds: 0,
    };
  },

  computed: {
    _second() {
      return 1000;
    },

    _minute() {
      return this._second * 60;
    },
    _hour() {
      return this._minute * 60;
    },
    _day() {
      return this._hour * 24;
    },
  },

  methods: {
    Time() {
      const timer = setInterval(() => {
        const now = new Date();
        const target = new Date(2023, 4, 23);
        const getTarget = target.getTime() - now.getTime();

        if (getTarget < 0) {
          clearInterval(timer);
          return;
        }

        const day = Math.floor(getTarget / this._day);
        const hour = Math.floor((getTarget % this._day) / this._hour);
        const minute = Math.floor((getTarget % this._hour) / this._minute);
        const second = Math.floor((getTarget % this._minute) / this._second);

        this.Minutes = minute < 10 ? "0" + minute : minute;
        this.Seconds = second < 10 ? "0" + second : second;
        this.Hours = hour < 10 ? "0" + hour : hour;
        this.Days = day < 10 ? "0" + day : day;
      }, 1000);
    },
  },
  mounted() {
    this.Time();
  },
};
</script>

<style></style>
