<template>
  <h3>About</h3>
  <p>Simple vue tutorial </p>
  <p>Version 1.0.0</p>
  <router-link to="/">Back to tasks</router-link>
</template>

<script> 
export default {
  name: 'About',
  inheritAttrs: false, // disable 'non-props' warning
};
</script>