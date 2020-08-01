<script>
	export let dataForTable;
	export let searchBy;
	export let searchByAll = false;
	export let disableAutoComplete = false;
	export let makeTableSortable = false;
	let inputcomponent='';
	let tableComponent;
	let getKeyFromJsonObject = Object.keys(dataForTable[0]);
	searchBy = searchBy ? searchBy : getKeyFromJsonObject[0];
	let selectedValue = searchByAll ? getKeyFromJsonObject[0] : searchBy;
	let ascendingIcon = '▲';
  let descendingIcon = '▼';
	let sortTheTable = {
		"id":getKeyFromJsonObject[0],
		"orderTable":1
	};
	function isNumber(number){
		if(isNaN(number))
			return false;
		return true;
	}
	function sortTable(column){
		if(sortTheTable.id === column)
			sortTheTable.orderTable = -1 * sortTheTable.orderTable;
		else
			sortTheTable.orderTable = 1;
		sortTheTable.id = column;
		let sortLogic = (a, b) => 
			(isNumber(dataForTable[0][column]) ? ( Number(a[column]) < Number(b[column]) ) : (a[column] < b[column]))
			? -1 * sortTheTable.orderTable 
			: (isNumber(dataForTable[0][column]) ? ( Number(a[column]) > Number(b[column]) ) : (a[column] > b[column])) 
			? 1 * sortTheTable.orderTable 
			: 0;
		dataForTable  = dataForTable.sort(sortLogic);
	}
</script>
<style>
	.showrow{
		display:auto;
	}
	.hiderow{
		display:none;
	}
	.maindiv{
		width:100%;
	}
	.maindiv span{
		font-weight:500;
	}
	table td{
		padding:5px 10px;
	}
	table thead{
		background:#e3e3e3;
		font-weight:500;
		text-transform:capitalize;
	}
	select , option{
		cursor:pointer;
		text-transform:capitalize;
	}
	td span{
		text-align:right;
		margin-left:15px;
		color:gray;
		font-size:small;
	}
	.changeColor{
		color:indianred;
		font-weight:bold;
	}
</style>
<div class='maindiv'>
	{#if !disableAutoComplete}
		<span>Search by : </span>
			{#if searchByAll}
			<select bind:value={selectedValue}>
				{#each getKeyFromJsonObject as rowkey}
					<option value={rowkey}>{rowkey}</option>
				{/each}
			</select> 
		{:else}
			<span>{searchBy}</span>
		{/if}
		<input type=text bind:value={inputcomponent} placeholder='Type to search'/>
	{/if}
	<table border="1" style='border-collapse:collapse' bind:this={tableComponent}>
		<thead>
			<tr style={makeTableSortable ? 'cursor:pointer' : ''}>
				{#each getKeyFromJsonObject as rowkey}
					<td on:click={()=>{if(makeTableSortable) sortTable(rowkey) }}>{rowkey} 
						{#if makeTableSortable}
							<span class={rowkey === sortTheTable.id ? 'changeColor' : ''}>
								{#if rowkey === sortTheTable.id}
									{sortTheTable.orderTable === 1 ? ascendingIcon : descendingIcon}
								{:else}
									{ascendingIcon}
								{/if}
							</span>
						{/if}
					</td>
				{/each}
			</tr>
		</thead>
		<tbody>
			{#each dataForTable as key}
					<tr class={key[selectedValue].toString().toLowerCase().includes(inputcomponent.toLowerCase()) ? 'showrow' : 'hiderow'}>
						{#each getKeyFromJsonObject as rowkey}
							<td>{key[rowkey]}</td>
						{/each}
					</tr>
			{/each}
		</tbody>
	</table>
</div>
