<script>
  import Editor from "./pages/Editor.svelte";
  import TemplatesList from "./pages/TemplatesList.svelte";
  // import { store_survey } from './stores.js';
  let url = "http://192.168.20.35:8000";

  if (location.hostname == 'localhost') {
    url = "http://192.168.20.35:8000";
  }
  else {
    url = location.host + 'survey-editor'
    console.log(url)
  }


  console.log(location.host)
</script>

<div class="grid-container">
  <TemplatesList {url}/>

  <Editor />

</div>


<style>
  .grid-container {
    display: grid;
    grid-template-columns: 1fr 5fr;
    grid-template-rows: 1fr;
    gap: 15px 15px;
  }
</style>
