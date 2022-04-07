<script>
  import MeetupItem from "./MeetupItem.svelte";
  export let meetups;
</script>

<section>
  {#each meetups as meetup}
    <MeetupItem
      id={meetup.id}
      title={meetup.title}
      subtitle={meetup.subtitle}
      description={meetup.description}
      image={meetup.imageUrl}
      address={meetup.address}
      contactEmail={meetup.contactEmail}
      isFav={meetup.isFavorite}
      on:togglefavorite
    />
  {/each}
</section>
