<script lang="ts">
	import { TrendingUp } from '@lucide/svelte';

	let { title = 'StockFlow' }: { title?: string } = $props();
</script>

<header class="h-16 bg-white border-b border-slate-200 sticky top-0 z-10 flex items-center justify-between px-6">
	<div class="flex items-center gap-2">
		<TrendingUp class="size-6 text-primary" />
		<h2 class="text-lg font-semibold text-slate-800">{title}</h2>
	</div>

	<div class="flex items-center gap-4">
		<div class="w-8 h-8 rounded-full bg-slate-200 flex items-center justify-center text-sm font-medium text-slate-600">
			U
		</div>
	</div>
</header>
