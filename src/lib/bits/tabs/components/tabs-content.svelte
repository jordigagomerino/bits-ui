<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { getCtx, getAttrs } from "../ctx.js";
	import type { ContentProps } from "../types.js";

	type $$Props = ContentProps;

	export let value: $$Props["value"];
	export let asChild: $$Props["asChild"] = false;

	const {
		elements: { content }
	} = getCtx();
	const attrs = getAttrs("content");

	$: builder = $content(value);
	$: Object.assign(builder, attrs);
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<div use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{/if}
