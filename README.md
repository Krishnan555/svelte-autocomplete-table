# svelte-autocomplete-table

Table with autocomplete , sorting and filtering based on column values.

## Install

```sh
npm install -save svelte-autocomplete-table
```

# Usage

This displays Table with AutoComplete feature , sorting feature.
 
```html

<script>
  import SvelteAutoCompleteTable from "svelte-autocomplete-table";
  const data = [
    /** data */
  ];
</script>

<SvelteAutoCompleteTable dataForTable={data} searchByAll makeTableSortable/>
```

This displays Table with AutoComplete feature with specific key , sorting feature.
 
```html
<script>
  import SvelteAutoCompleteTable from "svelte-autocomplete-table";
  const data = [
    /** data */
  ];
  const key = "Enter the key to Search in AutoComplete";
</script>

<SvelteAutoCompleteTable dataForTable={data} searchBy={key} makeTableSortable/>
```

This displays Table without AutoComplete feature.
 
```html
<script>
  import SvelteAutoCompleteTable from "svelte-autocomplete-table";
  const data = [
    /** data */
  ];
</script>

<SvelteAutoCompleteTable dataForTable={data} disableAutoComplete makeTableSortable/>
```

This displays Table without AutoComplete and sorting Feature.

```html
<script>
  import SvelteAutoCompleteTable from "svelte-autocomplete-table";
  const data = [
    /** data */
  ];
</script>

<SvelteAutoCompleteTable dataForTable={data} />
```


## Props

| Option              	| Type         | Description                                    |
| --------------------	| ------------ | ---------------------------------------------- |
| `dataForTable`      	| Object[]     | Data For Table			                |
| `searchBy`          	| String       | To make AutoComplete Search for particular key |
| `searchByAll`       	| Boolean      | To allow AutoComplete Search for all keys      |
| `makeTableSortable` 	| Boolean      | Whether the table can be sorted on column      |
| `disableAutoComplete` | Boolean      | Whether the table can have autocomplete or not	|

