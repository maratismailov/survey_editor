<script>
  export let survey;
  export let element;
  export let column;
  export let submit_element;
</script>


<style>
  .form_element {
    display: flex;
  }
  .form_left {
    width: 170px;
  }
  .form_right {
    flex-grow: 1;
  }
  .select_type {
    display: flex;
  }
  .type_radio {
    margin: 5px;
  }
</style>

<form on:submit|preventDefault={submit_element}>
  <div class="form_element">
    <div class="form_left">survey id</div>
    <div class="form_right">
      <input bind:value={survey.survey_id} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">survey name ru</div>
    <div class="form_right">
      <input bind:value={survey.name_ru} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">survey name en</div>
    <div class="form_right">
      <input bind:value={survey.name_en} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">survey name kg</div>
    <div class="form_right">
      <input bind:value={survey.name_kg} type="text" />
    </div>
  </div>
</form>
<hr />
<form on:submit|preventDefault={submit_element}>
  <div class="form_element">
    <div class="form_left">element id</div>
    <div class="form_right">
      <input bind:value={element.id} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">element name ru</div>
    <div class="form_right">
      <input bind:value={element.name_ru} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">element name en</div>
    <div class="form_right">
      <input bind:value={element.name_en} type="text" />
    </div>
  </div>

  <div class="form_element">
    <div class="form_left">element name kg</div>
    <div class="form_right">
      <input bind:value={element.name_kg} type="text" />
    </div>
  </div>

  <div>
    {#if element.type == 'table'}
      <div>fields:</div>
      <div>
        <input bind:value={column.id} placeholder="name" type="text" />
        <div id="select_type" class="select_type">
          <label class="type_radio">
            <input type="radio" bind:group={column.type} value={'text'} />
            text
          </label>
          <label class="type_radio">
            <input type="radio" bind:group={column.type} value={'number'} />
            number
          </label>
          <label class="type_radio">
            <input type="radio" bind:group={column.type} value={'select'} />
            select
          </label>
          <button type="button" on:click={add_column}>add column</button>
          <button type="submit" style="margin-left: 5px">Submit</button>
        </div>
      </div>
    {/if}
  </div>
  {#if element.type != 'table'}
    <div class="select_type">
      <label class="type_radio">
        <input type="radio" bind:group={element.type} value={'text'} />
        text
      </label>
      <label class="type_radio">
        <input type="radio" bind:group={element.type} value={'number'} />
        number
      </label>
      <label class="type_radio">
        <input type="radio" bind:group={element.type} value={'select'} />
        select
      </label>
      <label class="type_radio">
        <input type="radio" bind:group={element.type} value={'table'} />
        table
      </label>
      <button type="submit">Submit</button>
    </div>
  {/if}
</form>
