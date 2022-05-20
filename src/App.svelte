<script>
  import { marked } from "marked";
  let bionicMode = false;
  let text =
    "Bionic Reading is a new method facilitating the reading process by guiding the eyes through text with artificial fixation points. As a result, the reader is only focusing on the highlighted initial letters and lets the brain center complete the word. In a digital world dominated by shallow forms of reading, Bionic Reading aims to encourage a more in-depth reading and understanding of written content.";

  let footer =
    "v0.1. Created by [Simon Caine](https://twitter.com/smimons).\n\nThis app is inspired by, but in no way affiliated, associated, authorized, endorsed by, or in any way officially connected to [bionic-reading.com](https://bionic-reading.com) or its creator, [Renato Casutt](https://twitter.com/renato_casutt).";

  const formatText = (text) => {
    return splitAndFilter(text, "\n").map(formatParagraph).join("\n\n");
  };

  const formatParagraph = (paragraph) => {
    return splitAndFilter(paragraph, " ").map(formatWord).join(" ");
  };

  const formatWord = (word) => {
    let midpoint = word.length <= 3 ? 1 : Math.round(word.length / 2);
    return `<b>${word.substr(0, midpoint)}</b>${word.substr(midpoint)}`;
  };

  const hasLength = (entity) => entity?.length > 0;
  const splitAndFilter = (text, separator) =>
    text.split(separator).filter(hasLength);
</script>

<main>
  <h1><b>Bio</b>nic <b>Rea</b>der</h1>
  <label disabled={text.length === 0}>
    <input type="checkbox" bind:checked={bionicMode} />
    View in Bionic Mode
  </label>

  <div class="body">
    {#if !!bionicMode}
      <div class="bionicContainer">
        {@html marked(formatText(text))}
      </div>
    {:else}
      <textarea bind:value={text} />
    {/if}
  </div>

  <footer>{@html marked(footer)}</footer>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: none;
    margin: 0 auto;
    font-size: 1.2rem;
    color: #444;
  }

  input[type="checkbox"] {
    transform: scale(1.5);
    margin-right: 0.5rem;
  }

  h1 {
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
    margin: 0.5rem 0;
  }

  .body {
    width: clamp(55%, 1024px, 100%);

    margin: 0 auto;
  }

  .bionicContainer {
    text-align: left;
    min-height: 72vh;
    margin: 0 0.5rem;
  }

  textarea {
    margin-top: 0.3rem;
    width: 100%;
    resize: none;
    height: 72vh;
    color: #333;
  }

  footer {
    font-size: 0.65em;
  }
</style>
