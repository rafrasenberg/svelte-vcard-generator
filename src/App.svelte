<script>
  import Navbar from "./app/Sections/Navbar.svelte";
  import Footer from "./app/Sections/Footer.svelte";
  import Form from "./app/UI/Form.svelte";
  import VCard from "./app/Sections/VCard.svelte";

  let QRCode = false;
  let values;

  function getDispatchedProperty(prop) {
    QRCode = prop.detail;
  }
</script>

<Navbar title="Svelte.js vCard Generator" />

<main>
  <Form 
  bind:values on:createQRCode={getDispatchedProperty} />
  <VCard {values} {QRCode} />
</main>

<Footer />

<style global lang="scss">
	main {
	  padding: 1rem;
	  max-width: 600px;
    margin: 0 auto;
	}
</style>
