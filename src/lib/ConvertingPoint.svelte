<script>
  let {active = false, size = "50px"} = $props();

</script>

<div class="point" class:active={active} style="height: {size}; width: {size};"></div>

<style>
.point {
  margin: 5px;
  border-radius: 100%;
  background: linear-gradient(var(--color-bg-dark-start), var(--color-bg-dark-end));
  transition: all 0.5s ease;
}

.point.active {
  background: linear-gradient(var(--color-accent-1), var(--color-accent-1-90-50));
  transform: rotate(45deg) scale(0.75);
  border-radius: 0%;
  filter: drop-shadow(0 0 0.25rem var(--color-accent-1));
}
</style>
