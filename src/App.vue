<template>
  <div id="app">
    <h1>Добро пожаловать в мой Telegram WebApp!</h1>
    <button @click="onButtonClick">Нажми на меня!</button>
  </div>
</template>

<script>
export default {
  mounted() {
    const tg = window.Telegram.WebApp;
    tg.ready(); // Убедитесь, что WebApp API готов
    console.log('User data:', tg.initDataUnsafe);
  },
  methods: {
    onButtonClick() {
      alert('Кнопка нажата!');
    },
  },
};
</script>

<style lang="scss"scoped>
/* Ваши стили */
</style>