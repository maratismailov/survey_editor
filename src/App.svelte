<script>
  import Editor from "./pages/Editor.svelte";
  import TemplatesList from "./pages/TemplatesList.svelte";
  import Parsed from "./components/Parsed.svelte";
  import { survey } from './stores.js';

  const url = "http://192.168.20.35:8000";
</script>

<div class="grid-container">
  <TemplatesList {url}/>

  <Editor {url} {survey} />

  <Parsed />
</div>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: 1fr 3fr 2fr;
    grid-template-rows: 1fr;
    gap: 5px 5px;
  }
</style>
