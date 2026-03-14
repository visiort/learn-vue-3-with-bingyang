<template>
  <BaseLayout>
    <template #header>
      <h1>
        Here might be a page title.
      </h1>
    </template>

    <template #main>
      <p>
        A paragraph in the main content area.
      </p>
      <p>
        And another one.
      </p>
    </template>
 
    <template #footer>
      <p>
        Here is some contact information.
      </p>
    </template>
  </BaseLayout>
</template>

<script setup>
import BaseLayout from './BaseLayout.vue'
</script>

<style  scoped>

</style>