<script>
  import { createEventDispatcher } from "svelte";
  import TextInput from "../UI/TextInput.svelte";
  import Button from "../UI/Button.svelte";
  import Modal from "../UI/Modal.svelte";
  import { isEmpty } from "../helpers/validation";

  let title = "";
  let titleValid = false;
  let subtitle = "";
  let address = "";
  let email = "";
  let description = "";
  let imageUrl = "";
  let formIsValid = false;

  const dispatch = createEventDispatcher();

  $: titleValid = !isEmpty(title);

  const submitForm = () => {
    dispatch("save", {
      title,
      subtitle,
      address,
      email,
      description,
      imageUrl,
    });
  };

  const cancel = () => {
    dispatch("cancel");
  };
</script>

<Modal title="Edit Meetup Data" on:cancel>
  <form on:submit|preventDefault={() => submitForm()}>
    <TextInput
      id="title"
      label="Title"
      valid={titleValid}
      validityMessage={"Please enter a valid title."}
      value={title}
      on:input={(event) => (title = event.target.value)}
    />
    <TextInput
      id="subtitle"
      label="Subtitle"
      valid={!isEmpty(subtitle)}
      validityMessage={"Please enter a valid subtitle."}
      value={subtitle}
      on:input={(event) => (subtitle = event.target.value)}
    />
    <TextInput
      id="address"
      label="Address"
      valid={!isEmpty(address)}
      validityMessage={"Please enter a valid address."}
      value={address}
      on:input={(event) => (address = event.target.value)}
    />
    <TextInput
      id="imageUrl"
      label="Image URL"
      valid={!isEmpty(imageUrl)}
      validityMessage={"Please enter a valid image url."}
      value={imageUrl}
      on:input={(event) => (imageUrl = event.target.value)}
    />
    <TextInput
      id="email"
      label="E-Mail"
      type="email"
      value={email}
      validityMessage={"Please enter a valid email."}
      valid={!isEmpty(email)}
      on:input={(event) => (email = event.target.value)}
    />
    <TextInput
      id="description"
      label="Description"
      controlType="textarea"
      valid={!isEmpty(description)}
      validityMessage={"Please enter a valid description."}
      value={description}
      on:input={(event) => (description = event.target.value)}
    />
    <Button on:click={cancel} slot="footer" mode="outline">Close</Button>
    <Button type="submit" slot="footer">Save</Button>
  </form>
</Modal>

<style>
  form {
    width: 100%;
  }
</style>
