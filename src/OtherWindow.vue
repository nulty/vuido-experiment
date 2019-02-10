<template>
  <Window title="weatherornot" width="400" height="100" margined v-on:close="close">
    <Box padded>
      <Text>
        {{ userName }}
      </Text>
    </Box>
  </Window>
</template>

<script>
export default {
  props: ['userName'],
  computed: {

  },
  methods: {
    close() {
      this.$root.$destroy();
    }
  }
}
</script>
