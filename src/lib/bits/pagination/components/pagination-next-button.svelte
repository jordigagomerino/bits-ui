<script lang="ts">
	import type { NextButtonEvents, NextButtonProps } from "../types.js";
	import { createDispatcher } from "$lib/internal/events.js";
	import { getAttrs, getCtx } from "../ctx.js";
	import { melt } from "@melt-ui/svelte";

	type $$Props = NextButtonProps;
	type $$Events = NextButtonEvents;

	export let asChild: $$Props["asChild"] = undefined;

	const {
		elements: { nextButton }
	} = getCtx();

	const attrs = getAttrs("next-button");

	$: builder = $nextButton;
	$: Object.assign(builder, attrs);

	const dispatch = createDispatcher();
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<button
		use:melt={builder}
		type="button"
		{...$$restProps}
		on:m-click={dispatch}
	>
		<slot {builder} />
	</button>
{/if}
