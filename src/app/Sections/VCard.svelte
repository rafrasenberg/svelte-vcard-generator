<script>
  import Flex from "../Layout/Flex.svelte";

  export let QRCode = false;
  export let values = {
    name: "",
    organisation: "",
    jobTitle: "",
    phone: "",
    address: "",
    email: "",
    photoURL: "",
  };

  $: qrString = 
    `BEGIN:VCARD
    VERSION:4.0
    N:${values.name};${values.name};;;
    FN:${values.name}
    ORG:${values.organisation}
    TITLE:${values.jobTitle}
    TEL;TYPE=work;VALUE=uri:${values.phone}
    ADR;TYPE=WORK;PREF=1;LABEL="${values.address}":;;${values.address}
    EMAIL;TYPE=WORK:${values.email}
    REV:20080424T195243Z
    x-qq:21588891
    END:VCARD`;

</script>

<section>
  <Flex justify={'space-between'} align={'start'}>
    <Flex direction={'column'}>
      
      {#if values.photoURL}
      <picture>
        <img id="photo" src={values.photoURL} alt="avatar" />
      </picture>
      {/if}
      
      {#if values.name}
      <h1>{values.name}</h1>
      {/if}

      {#if values.jobTitle}
      <h3>{values.jobTitle}</h3>
      {/if}

      {#if values.phone}
      <Flex>
        <picture class="logo">
          <img
            src="https://icongr.am/entypo/old-phone.svg?size=20&color=ffffff"
            alt="phone" />
        </picture>
        <span>{values.phone}</span>
      </Flex>
      {/if}

      {#if values.address}
      <Flex>
        <picture class="logo">
          <img
            src="https://icongr.am/entypo/address.svg?size=20&color=ffffff"
            alt="address" />
        </picture>
        <span>{values.address}</span>
      </Flex>
      {/if}

      {#if values.email}
      <Flex>
        <picture class="logo">
          <img
            src="https://icongr.am/entypo/email.svg?size=20&color=ffffff"
            alt="email" />
        </picture>
        <span><a href="mailto:{values.email}">{values.email}</a></span>
      </Flex>
      {/if}

    </Flex>
    <Flex direction={'column'} align={'end'}>
      <Flex align="center">
        {#if values.organisation}
        <h2>{values.organisation}</h2>
        {/if}
      </Flex>

      {#if QRCode}
        <picture id="qrcode">
          <img
            src={`https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=${encodeURI(qrString)}`}
            alt="qrcode" />
        </picture>
      {/if}

    </Flex>
  </Flex>
</section>

<style lang="scss">
  section {
    width: 600px;
    height: 370px;
    padding: 2rem 2rem;
    margin: 2rem auto 5rem auto;
    border-radius: 10px;
    position: relative;
    color: white;
    background-color: $color-1;
    background-size: cover;
  }
  h1 {
    color: $white;
    text-transform: uppercase;
  }
  h2 {
    color: $white;
  }
  .logo {
    margin: 0.5rem 0.5rem 0.5rem 0;
    position: relative;
    top: 5px;
  }
  #photo {
    /* margin-top: 0.8rem; */
    border-radius: 50%;
    height:6rem;
    border: 2px solid $white;
  }
  #qrcode {
    margin-top: 5rem;
  }
</style>