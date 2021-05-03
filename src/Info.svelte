<script>
  // täällä ei kummempia, tekija välitetään propsina ja h1 stylet
  export let tekija;
</script>

<section>
  <h1>{tekija}n maaginen lottorivi generaattori</h1>
  <h2>Lisää arvottava rivi ja klikkaa "Aloita arvonta"!</h2>
</section>

<style>
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
</style>
