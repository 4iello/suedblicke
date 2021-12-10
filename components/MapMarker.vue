<template>
  <g id="Marker">
    <circle
      :for="marker in marker"
      :key="marker.id"
      r="10"
      :cx="marker[0][0]"
      :cy="marker[0][1]"
    />
  </g>
</template>
<script>
export default {
  data() {
    return {
      marker: [
        {
          position: [10, 20],
          id: 1,
        },
        { position: [40, 100], id: 2 },
      ],
    }
  },
}
</script>
<style></style>
