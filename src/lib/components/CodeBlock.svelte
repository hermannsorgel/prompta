<script lang="ts">
  import { onMount } from "svelte";
  import { dirname } from "$lib/utils";
  import Prism from "prismjs";
  import "prismjs/themes/prism-tomorrow.css"; // Choose a theme of your liking
  import "prismjs/plugins/autoloader/prism-autoloader";
  import "prismjs/plugins/line-numbers/prism-line-numbers";
  import "prismjs/plugins/line-numbers/prism-line-numbers.css";
  import prismPath from "prismjs/components/?url";

  // Seems like there woudl be a more direct way to do this...
  Prism.plugins.autoloader.languages_path = dirname(prismPath) + "/";

  export let lang = "";
  export let text = "";

  let codeElement: HTMLElement;

  const handleHighlight = () => {
    if (codeElement && lang && text) {
      console.debug("Prism.highlight", { lang, text, codeElement });
      Prism.highlightElement(codeElement);
    }
  };

  onMount(() => {
    handleHighlight();
  });
</script>

<pre class="language-{lang}"><code bind:this={codeElement} class="language-{lang}">{text}</code
  ></pre>