<script>
  export let onkoArvottu;
  export let name;
</script>

<section>
  {#if onkoArvottu === true}
    <p>Anna maagiselle riville nimi:</p>
    <input type="text" bind:value={name} />
  {:else}
    <p>Arvo ensin rivi niin saat lisävaihtoehtoja.</p>
  {/if}
</section>

<style>
  p {
    color: #ff3e00;
    font-size: 20px;
  }
</style>
