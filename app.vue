<template>
  <div class="fullpage">
    <TheHeader></TheHeader>

    <NuxtPage />

    <TheFooter></TheFooter>
  </div>
</template>
<style lang="scss">
.fullpage {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
}

.ql-editor {
  height: 200px !important;
  border-radius: 10px !important;
  background: #F6FAFF !important;
  /* Например, 300px */
}

.ql-editor {
  border: 1px solid #D2D2D2 !important;
  border-radius: 0 !important;
  border-top-left-radius: 0 !important;
  border-top-right-radius: 0 !important;
}

.ql-container.ql-snow {
  border: 0 !important;
}

.ql-toolbar.ql-snow {
  border: 1px solid #D2D2D2 !important;
  border-radius: 0 !important;
  border-bottom-right-radius: 0 !important;
  border-bottom-left-radius: 0 !important;
}

input ::placeholder {
  color: #000 !important;
}

h1,
h2,
h3,
h4,
h5,
h6,
span,
p,
a,
small,
div,
li,
button,
input,
textarea {
  font-variant-numeric: lining-nums proportional-nums !important;
}
</style>
