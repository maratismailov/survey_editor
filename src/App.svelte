<script>
  import { onMount } from "svelte";

  import Editor from "./pages/Editor.svelte";
  import TemplatesList from "./pages/TemplatesList.svelte";
  // import { store_survey } from './stores.js';
  let url = "http://192.168.20.35:8000";

  if (location.hostname == "localhost") {
    url = "http://192.168.20.35:8000";
  } else {
    url = "https://" + location.host + "/survey-editor";
  }

  onMount(async () => {
    const res = await fetch('https://dev.forest.caiag.kg/ru/rent/taxdescr/getdictionarysurveyeditor');
    const dictionary = await res.json();
    console.log(dictionary)
  });
</script>

<div class="grid-container">
  <TemplatesList {url} />

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
