<script>
  //täältäkin välitetään ensin pari propsia
  export let onkoArvottu;
  export let name;
  export let isValid;
</script>

<section>
  <!-- ja täällä if-lohko joka mahdolistaa rivin nimeämisen jos se on arvottu
  plus input fieldin validointi-->
  {#if onkoArvottu === true}
    <p>Anna maagiselle riville nimi:</p>
    <input type="text" bind:value={name} class:tyhja={!isValid} />
  {:else}
    <p>Arvo ensin rivi niin saat lisävaihtoehtoja.</p>
  {/if}
</section>

<style>
  p {
    color: #ff3e00;
    font-size: 20px;
  }

  .tyhja {
    border: 1px solid red;
    background-color: rgb(255, 75, 75);
  }
</style>
