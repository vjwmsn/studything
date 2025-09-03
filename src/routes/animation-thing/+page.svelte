<script>
  import TextButton from "$lib/TextButton.svelte";
  import ConvertingPoint from "$lib/ConvertingPoint.svelte";

  let active = $state(false);

  function changeState() {
    active = !active;
  }
</script>

<div class="point" class:active={active}></div>

<TextButton content="Press me to toggle the animation!" onClick={changeState}/>

<ConvertingPoint active={active}/>

<style>
.point {
  height: 50px;
  width: 50px;
  margin: 20px;
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
