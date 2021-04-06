<script>
    export let element;
</script>

    <div>
        <div>select:</div>
        <div class="form_element">
            <div class="form_left">table name</div>
            <div class="form_right">
                <input bind:value={element.select.table_name} type="text" />
            </div>
        </div>

        <div class="form_element">
            <div class="form_left">name column</div>
            <div class="form_right">
                <input bind:value={element.select.name_column} type="text" />
            </div>
        </div>

        <div class="form_element">
            <div class="form_left">id column</div>
            <div class="form_right">
                <input bind:value={element.select.id_column} type="text" />
            </div>
        </div>

        <div class="form_element">
            <div class="form_left">where clause</div>
            <div class="form_right">
                <input bind:value={element.select.where_clause} type="text" />
            </div>
        </div>
    </div>

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
</style>
