<template>
  <main>
    <h1>GeoJSON API Frontend</h1>
    <div>
      <p>
        This web application retrieves earthquake data from the USGS feed and displays it in a user friendly manner.
      </p>
      <h2>Usage</h2>
      <p>
        To get started, just input a page number, the number of features per page you want to see and mark the magnitudes to want to filter, if any.
      </p>
      <div class="contact">
        <p>Made by Luis Felipe Azócar for Frogmi's Technical Challenge.</p>
        <a href="https://github.com/lfazocar" target="_blank">
          <div class="github-logo"></div>
        </a>
      </div>
    </div>
  </main>
</template>

<style scoped>
.contact {
  text-align: center;
}

.github-logo {
  background-image: url(/github-mark-white.svg);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  display:inline-block;
  width: 100px;
  height: 100px;
}

@media (prefers-color-scheme: light) {
  .github-logo {
    background-image: url(/github-mark.svg);
  }
}
</style>
