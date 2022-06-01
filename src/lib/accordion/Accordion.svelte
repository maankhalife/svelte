<script>

	import Body from './body.svelte';
	import Item from './item.svelte';

	export let id = "0";

    export let title = "";
    
    export let subTitle = "";

	export let content = "";

	export let active = "-1";

</script>

<Body bind:active>
	<Item id="{id}" title="{title}" subTitle="{subTitle}">
		<h3>
			{content}
		</h3>
	</Item> 
</Body>