<script>
  //täältäkin välitetään ensin pari propsia
  export let onkoArvottu;
  export let name;
</script>

<section>
  <!-- ja täällä if-lohko joka mahdolistaa rivin nimeämisen jos se on arvottu-->
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
