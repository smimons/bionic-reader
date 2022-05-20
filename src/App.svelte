<script>
  import { marked } from "marked";
  let bionicMode = false;
  let text = "";

  let footer =
    "**v0.1.** Created by [Simon Caine](https://twitter.com/smimons). Based on the [Bionic Reading](https://bionic-reading.com) concept by [Renato Casutt](https://twitter.com/renato_casutt).";

  function convertToBionic(text) {
    return text.split(" ").map((word) => {
      let midpoint = Math.ceil(word.length / 2);
      return `**${word.substr(0, midpoint)}**${word.substr(midpoint)}`;
    });
  }
</script>

<main>
  <h1><b>Bionic</b> Reader</h1>
  <p>
    An unofficial Bionic Reading 'translator'. Learn more at <a
      href="https://bionic-reading.com/">bionic-reading.com</a
    >.
  </p>

  <label disabled={text.length === 0}>
    <input
      type="checkbox"
      bind:checked={bionicMode}
      disabled={text.length === 0}
    />
    View in Bionic Mode
  </label>

  <div class="body">
    {#if !!bionicMode}
      <div class="bionicContainer">
        {@html marked(convertToBionic(text))}
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
    max-width: 480px;
    margin: 0 auto;
    font-size: 1.2rem;
  }

  input[type="checkbox"] {
    transform: scale(1.5);
    margin-right: 0.5rem;
  }

  a {
    font-weight: bold;
  }

  h1 {
    color: #333333;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
    margin: 0.5rem 0;
  }

  .body {
    width: 90%;
    margin: 0 auto;
  }

  .bionicContainer {
    text-align: left;
    color: #222222;
  }

  textarea {
    width: 100%;
    resize: none;
    height: 640px;
  }

  footer {
    font-size: 0.75em;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }

    .body {
      width: 70%;
      margin: 0 auto;
    }
  }
</style>
