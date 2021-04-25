<template>
  <div class="page">
    <div class="page-header">
      <div class="container">
        <a href="/" class="d-block">
          <Logo />
        </a>
      </div>
    </div>
    <div class="page-content">
      <Nuxt />
    </div>
  </div>
</template>

<style>
html {
  font-size: 16px;
}

body {
  background-color: #F0F0F2;
}

.page-header {
  background-color: white;
  padding: 1rem 0;
}

.page-content {
  padding: 0 0 3rem 0;
}
</style>
