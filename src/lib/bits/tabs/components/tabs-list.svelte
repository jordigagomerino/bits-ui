<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { getCtx, getAttrs } from "../ctx.js";
	import type { ListProps } from "../types.js";

	type $$Props = ListProps;

	export let asChild: $$Props["asChild"] = false;

	const {
		elements: { list }
	} = getCtx();

	const attrs = getAttrs("list");

	$: builder = $list;
	$: Object.assign(builder, attrs);
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<div use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{/if}
