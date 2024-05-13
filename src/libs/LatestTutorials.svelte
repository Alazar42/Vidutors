<script>
  export let currentPage;
  let latestTutorials = [
    {
      id: 0,
      title: "Svelte Tutorial for Beginners",
      description:
        "Hey gang, in this Svelte tutorial for beginners I'll explain what Svelte is, what we'll be making & what you'll already need to know before starting. ",
      videoURL: "test.mkv",
      timeStamp: "May-9-2024 G.C",
    },
    {
      id: 1,
      title: "Svelte Kit Tutorial for Beginners",
      description:
        "Hey micky, in this Svelte tutorial for beginners I'll explain what Svelte is, what we'll be making & what you'll already need to know before starting. ",
      videoURL: "test.mkv",
      timeStamp: "May-9-2024 G.C",
    },
    {
      id: 2,
      title: "Vue Tutorial for Beginners",
      description:
        "Hey vue, in this Svelte tutorial for beginners I'll explain what Svelte is, what we'll be making & what you'll already need to know before starting. ",
      videoURL: "test.mkv",
      timeStamp: "May-9-2024 G.C",
    },
  ];

  let isDescriptionHidden = true
  let currentDescription = "";
  let currentVideoURL = "";

  const showDescription = (id) => {
    isDescriptionHidden = !isDescriptionHidden
    if (isDescriptionHidden){
    latestTutorials.forEach((tutorial) => {
      if (id == tutorial.id) {
        currentDescription = tutorial.description;
        currentVideoURL = tutorial.videoURL;
      }
    });
  }else{
    currentDescription = ""
    currentVideoURL = ""
  }
};
</script>

{#if currentPage == "Home"}
  <div class="adwa-row-padding-64 adwa-center">
    <h1 class="adwa-row-padding adwa-red adwa-rightbar adwa-border-pale-red adwa-center">
      Latest Tutorials
    </h1>
  </div>

  <div class="adwa-row-padding-64">
    <div class="adwa-row-padding-64">
      {#each latestTutorials as tutorials}
        <div class="adwa-half adwa-padding">
          <h4>Title: {tutorials.title}</h4>
          <p>Date: {tutorials.timeStamp}</p>
          <button
            on:click={() => showDescription(tutorials.id)}
            class="adwa-button adwa-red adwa-hover-green adwa-right adwa-round"
            >{#if isDescriptionHidden && tutorials.description == currentDescription}Hide{:else}Description{/if}</button
          >
          {#if currentDescription != ""}
            {#if tutorials.description == currentDescription}
              <div class="adwa-padding">
                <p>Date: {currentDescription}</p>
                <video
                  style="width: 100%;"
                  class="adwa-image"
                  controls="1"
                  src={currentVideoURL}><track kind="captions" /></video
                >
              </div>
            {/if}
          {/if}
        </div>
      {/each}
    </div>
  </div>
{/if}
