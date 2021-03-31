<script>
  import { onMount } from 'svelte';
  import axios from "redaxios";
import { dataset_dev } from 'svelte/internal';

  export let element;
  let result = null

  const table_name = element.select.table_name;
  const name_column = element.select.name_column;
  const id_column = element.select.id_column;

  const query =
    '{  selectList(tableName:"' + table_name + '", nameColumn:"' + name_column + '", idColumn: "' + id_column +'") {    id    nameRu    nameEn    nameKg  }}';

  onMount(async () => {
    const res = await fetch(`http://192.168.20.35:8000/?query=` + query);
    result = await res.json();
    console.log(result)
  });

  let selected;

  const options = ["option1", "option2"];
</script>

<select bind:value={element.value}>
  {#if result}
  {#each result.data.selectList as option}
  <option>{option.nameRu}</option>
  {/each}
  {/if}
</select>
<br />
