<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { getCtx, getAttrs } from "../ctx.js";
	import type { InputProps } from "../types.js";

	type $$Props = InputProps;

	export let asChild: $$Props["asChild"] = false;

	const {
		elements: { hiddenInput },
		options: { disabled }
	} = getCtx();

	$: attrs = {
		...getAttrs("input"),
		disabled: $disabled ? true : undefined
	};

	$: builder = $hiddenInput;
	$: Object.assign(builder, attrs);
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<input use:melt={builder} {...$$restProps} />
{/if}
