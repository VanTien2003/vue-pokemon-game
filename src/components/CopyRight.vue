<template>
  <div class="copyright">
    <p>
      This game owned by Van Tien in Vue 3 -
      <a href="#">view here</a>
    </p>
  </div>
</template>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  background-color: var(--dark);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
