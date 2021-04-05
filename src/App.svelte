<script>
  import Editor from "./pages/Editor.svelte";
  import TemplatesList from "./pages/TemplatesList.svelte";
  import Parsed from "./components/Parsed.svelte";
  import CurrentElement from "./pages/CurrentElement.svelte"
  // import { store_survey } from './stores.js';

  const url = "http://192.168.20.35:8000";
</script>

<div class="grid-container">
  <TemplatesList {url}/>

  <Editor {url}/>

  <CurrentElement />
</div>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 3fr;
    grid-template-rows: 1fr;
    gap: 15px 15px;
  }
</style>
