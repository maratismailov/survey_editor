<script>
  import TextInput from "./TextInput.svelte";
  import NumberInput from "./NumberInput.svelte";
  import SelectInput from "./SelectInput.svelte";
  import Table from "./Table.svelte";

  export let survey;
</script>

<div class={$$props.class}>
  parsed
  {#if survey}
    {#each survey as element}
      <div>{element.id}</div>
      <div>{element.name}</div>
      {#if element.type === "text"}
        <TextInput {element} />
      {:else if element.type === "number"}
        <NumberInput {element} />
      {:else if element.type === "select"}
        <!-- <input bind:value={element.value} type="number" /> -->
        <SelectInput {element} />
      {:else if element.type === "table"}
        <Table {element} />
      {/if}
    {/each}
  {/if}
</div>

