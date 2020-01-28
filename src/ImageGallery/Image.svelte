<script>
  import { crossfade, scale } from "svelte/transition";
  import images from "./images.js";

  const [send, receive] = crossfade({
    duration: 200,
    fallback: scale
  });

  let selected = null;
  let loading = null;

  const ASSETS = `https://sveltejs.github.io/assets/crossfade`;

  const load = image => {
    const timeout = setTimeout(() => (loading = image), 100);

    const img = new Image();

    img.onload = () => {
      selected = image;
      clearTimeout(timeout);
      loading = null;
    };

    img.src = `${ASSETS}/${image.id}.jpg`;
  };
</script>

<style>
  .container {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
  }

  .phone {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 88%;
    height: 49%;
    padding: 3vmin;
    border-radius: 2vmin;
    margin-top: 77%;
  }

  h1 {
    font-weight: 300;
    text-transform: uppercase;
    font-size: 5vmin;
    margin: 0.2em 0 0.5em 0;
  }

  .grid {
    display: grid;
    flex: 1;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(4, 1fr);
    grid-gap: 2vmin;
  }

  .square {
    width: 100%;
    height: 100%;
    color: white;
    font-size: 5vmin;
    border: none;
    margin: 0;
    will-change: transform;
  }

  .photo,
  img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .photo {
    display: flex;
    align-items: stretch;
    justify-content: flex-end;
    flex-direction: column;
    will-change: transform;
  }

  img {
    object-fit: cover;
    cursor: pointer;
  }

  .credit {
    text-align: right;
    font-size: 2.5vmin;
    padding: 1em;
    margin: 0;
    color: white;
    font-weight: bold;
    opacity: 0.6;
    background: rgba(0, 0, 0, 0.4);
  }
	img{

	}
  .credit a,
  .credit a:visited {
    color: white;
  }
</style>

<div class="container">
  <div class="phone">
    <!-- <h1>Photo gallery</h1> -->

    <div class="grid">
      {#each images as image}
        <div class="square">
         {#if selected !== image}
            <img
              alt="{ASSETS}/{image.alt}"
              src="{ASSETS}/{image.id}.jpg"
              on:click={() => load(image)}
              in:receive={{ key: image.id }}
              out:send={{ key: image.id }} />
          {/if}
        </div>
      {/each}
    </div>

    {#if selected}
      {#await selected then d}
        <div class="photo" in:receive={{ key: d.id }} out:send={{ key: d.id }}>
          <img
            alt={d.alt}
            src="{ASSETS}/{d.id}.jpg"
            on:click={() => (selected = null)} />

          <p class="credit">
            <a target="_blank" href="https://www.flickr.com/photos/{d.path}">
              via Flickr
            </a>
            &ndash;
            <a target="_blank" href={d.license.url}>{d.license.name}</a>
          </p>
        </div>
      {/await}
    {/if}
  </div>
</div>
