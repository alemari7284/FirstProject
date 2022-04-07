<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import Button from "./UI/Button.svelte";

  export let title = "";
  export let subtitle = "";
  export let address = "";
  export let email = "";
  export let description = "";
  export let imageUrl = "";

  let meetups = [
    {
      id: "m1",
      title: "Coding Bootcamp",
      subtitle: "Learn to code in 2 hours",
      description:
        "In this meetup, we will have some experts that will teach you to code!",
      imageUrl:
        "https://www.sapere.it/.imaging/mte/sapere/624x410/dam/icone-sapere/approfondimenti/sapermangiare/caffe-dieta/jcr:content/caffe-dieta.jpg",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "code@test.com",
      isFavorite: false,
    },
    {
      id: "m2",
      title: "Something else",
      subtitle: "We'll figure something out",
      description: "It's just a description",
      imageUrl:
        "https://www.coind.it/wp-content/uploads/2017/08/caff%C3%A8.png",
      address: "27th Nerd Road, 32523 New York",
      contactEmail: "dontcode@test.com",
      isFavorite: false,
    },
  ];

  function addMeetup() {
    const newMeetup = {
      id: Math.random().toString(),
      title,
      subtitle,
      description,
      imageUrl,
      contactEmail: email,
      address,
    };

    const toggleFavorite = (event) => {
      const id = event.detail;
      const updatedMeetup = { ...meetups.find((m) => m.id === id) };
      updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
      const meetupIndex = meetups.findIndex((m) => m.id === id);
      const updatedMeetups = [...meetups];
      updatedMeetups[meetupIndex] = updatedMeetup;
      meetups = [...updatedMeetups];
    };

    meetups = [...meetups, newMeetup];
  }
</script>

<Header />
<main>
  <form on:submit|preventDefault={addMeetup}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      controlType=""
      type="text"
      on:input={(event) => (title = event.target.value)}
    />
    <TextInput
      id="subtitle"
      label="subtitle"
      value={subtitle}
      controlType=""
      type="text"
      on:input={(event) => (subtitle = event.target.value)}
    />
    <TextInput
      id="address"
      label="Address"
      value={address}
      controlType=""
      type="text"
      on:input={(event) => (address = event.target.value)}
    />
    <TextInput
      id="imageUrl"
      label="Image URL"
      value={imageUrl}
      controlType=""
      type="text"
      on:input={(event) => (imageUrl = event.target.value)}
    />
    <TextInput
      id="email"
      label="Email"
      value={email}
      controlType=""
      type="email"
      on:input={(event) => (email = event.target.value)}
    />
    <TextInput
      id="description"
      label="Description"
      value={description}
      controlType="textarea"
      rows="3"
      on:input={(event) => (description = event.target.value)}
    />
    <Button type="submit" caption="Save" />
  </form>
  <MeetupGrid {meetups} on:togglefavorite={toggleFavorite} />
</main>

<style>
  main {
    margin-top: 5rem !important;
  }

  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>
