<script>
export default {
  data() {
    return {
      started: false,
      text: "Empezamos en ",
      seconds: 3,
      times: 1,
    };
  },
  methods: {
    async start() {
      this.started = !this.started;
      await this.countDown();
      for (let i = 0; i < 20; i++) {
        await this.aspire();
        await this.wait();
        await this.exhale();
        await this.addTime();
      }
      this.stop();
    },
    async stop() {
      window.location.reload();
    },
    sleep(ms) {
      return new Promise((resolve) => {
        setTimeout(resolve, ms);
      });
    },
    async addTime() {
      await this.sleep(1000);
      this.times++;
    },
    async countDown() {
      for (let i = 0; i < 3; i++) {
        await this.sleep(1000);
        this.seconds--;
      }
    },
    async aspire() {
      this.text = "Aspira ";
      this.seconds = 4;
      for (let i = 0; i < 4; i++) {
        await this.sleep(1000);
        this.seconds--;
      }
    },
    async exhale() {
      this.text = "Exala ";
      this.seconds = 4;
      for (let i = 0; i < 4; i++) {
        await this.sleep(1000);
        this.seconds--;
      }
    },
    async wait() {
      this.text = "Espera ";
      this.seconds = 8;
      for (let i = 0; i < 8; i++) {
        await this.sleep(1000);
        this.seconds--;
      }
    },
  },
};
</script>

<template>
  <h1 class="text-center mt-3">Respiración profunda.</h1>
  <h2 class="text-center mt-3">
    Pequeña aplicacion para respires profundamente por 4s y mantenerlo 8s, 20
    veces.
  </h2>
  <div
    style="height: 80vh"
    class="d-flex justify-content-center align-items-center"
  >
    <button v-if="!started" class="btn btn-outline-light" @click="start">
      Iniciar
    </button>
    <div
      v-if="started"
      class="d-flex flex-column justify-content-center align-items-center"
    >
      <h3 class="mb-3">{{ times }}</h3>
      <h3 class="mb-3">{{ text }}{{ seconds }}s</h3>
      <button class="btn btn-outline-light mb-3" @click="stop">Parar</button>
    </div>
  </div>
</template>
