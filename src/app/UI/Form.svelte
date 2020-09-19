<script>
  import { createEventDispatcher, onMount } from "svelte";
  const dispatch = createEventDispatcher();

  export let values = {
    name: "",
    organisation: "",
    jobTitle: "",
    phone: "",
    address: "",
    email: "",
    photoURL: "https://rafrasenberg.com/images/profilepic.jpeg",
  };

  let disabled = true;
  let firstInput;

  let active = {
    name: false,
    organisation: false,
    jobTitle: false,
    phone: false,
    address: false,
    email: false,
    photoURL: false,
  };

  const inputsData = {
    name: {
      label: "Name",
      type: "text",
      placeholder: "Your contact name",
    },
    organisation: {
      label: "Organisation",
      type: "text",
      placeholder: "Name of your organisation",
    },
    jobTitle: {
      label: "Job Title",
      type: "text",
      placeholder: "Your job title",
    },
    phone: {
      label: "Phone number",
      type: "text",
      placeholder: "Your phone number",
    },
    address: {
      label: "Address",
      type: "text",
      placeholder: "Professional address",
    },
    email: {
      label: "E-Mail",
      type: "email",
      placeholder: "Professional E-Mail address",
    },
    photoURL: {
      label: "Photo",
      type: "text",
      placeholder: "URL of personal portrait",
    },
  };

  function resetClicked() {
    disabled = true;
    values = {
      name: "",
      organisation: "",
      jobTitle: "",
      phone: "",
      address: "",
      email: "",
      photoURL: "",
    };

    if(localStorage.getItem("values")) localStorage.removeItem("values");
    dispatch("createQRCode", false);
    firstInput.focus();
  }

  function keyPressed(event) {
    event.key === "Shift" ? "" : (disabled = false);
    dispatch("createQRCode", false);
  }

  function dispatchToParent() {
    localStorage.setItem('values', JSON.stringify(values));
    dispatch("createQRCode", true);
  }

  onMount(async () => {
    if (localStorage.getItem("values")) {
      values = JSON.parse(localStorage.getItem('values'));
    }
	});
</script>

<form>
  <label>
    <div class="labelText">
      {inputsData.name.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.name.placeholder}
      class:active={active.name}
      on:focus={() => {
        active.name = true;
      }}
      on:blur={() => {
        active.name = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.name}
      bind:this={firstInput} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.organisation.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.organisation.placeholder}
      class:active={active.organisation}
      on:focus={() => {
        active.organisation = true;
      }}
      on:blur={() => {
        active.organisation = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.organisation} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.jobTitle.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.jobTitle.placeholder}
      class:active={active.jobTitle}
      on:focus={() => {
        active.jobTitle = true;
      }}
      on:blur={() => {
        active.jobTitle = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.jobTitle} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.phone.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.phone.placeholder}
      class:active={active.phone}
      on:focus={() => {
        active.phone = true;
      }}
      on:blur={() => {
        active.phone = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.phone} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.address.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.address.placeholder}
      class:active={active.address}
      on:focus={() => {
        active.address = true;
      }}
      on:blur={() => {
        active.address = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.address} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.email.label}
    </div>
    <input
      type="email"
      placeholder={inputsData.email.placeholder}
      class:active={active.email}
      on:focus={() => {
        active.email = true;
      }}
      on:blur={() => {
        active.email = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.email} />
  </label>
  <label>
    <div class="labelText">
      {inputsData.photoURL.label}
    </div>
    <input
      type="text"
      placeholder={inputsData.photoURL.placeholder}
      class:active={active.photoURL}
      on:focus={() => {
        active.photoURL = true;
      }}
      on:blur={() => {
        active.photoURL = false;
      }}
      on:keydown={keyPressed}
      bind:value={values.photoURL} />
  </label>

  <article>
    <button {disabled} on:click|preventDefault={resetClicked}>Reset</button>
    <button on:click|preventDefault={dispatchToParent}>Create QR Code</button>
  </article>
</form>

<style lang="scss">
  label {
    display: flex;
    align-items: baseline;
    margin: 0.5rem;
    font-weight: bold;
  }
  input {
    width: 70%;
    margin: 0 0.5rem;
    border-radius: 5px;
  }
  article {
    display: flex;
    justify-content: space-evenly;
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
  button {
    margin: 0.5rem 0;
    cursor: pointer;
    border-radius: 5px;
  }
  .labelText {
    text-align: end;
    width: 30%;
  }
  .active {
    border-color: $black;
    box-shadow: 0 1px 5px $color-1;
  }
</style>
