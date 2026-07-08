<script lang="ts">
	import { Button } from '$lib/components/ui/button/index.js';

	const cards = [
		{ label: 'Total Stocks', value: '128' },
		{ label: 'Watchlist', value: '12' },
		{ label: 'Alerts', value: '3' }
	];
</script>

<div class="space-y-6">
	<div class="flex items-center justify-between">
		<h1 class="text-2xl font-bold text-slate-900">Dashboard</h1>
		<Button>Refresh</Button>
	</div>

	<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
		{#each cards as card}
			<div class="bg-white rounded-lg border border-slate-200 p-6 shadow-sm">
				<p class="text-sm font-medium text-slate-500">{card.label}</p>
				<p class="mt-2 text-3xl font-semibold text-slate-900">{card.value}</p>
			</div>
		{/each}
	</div>

	<div class="bg-white rounded-lg border border-slate-200 p-6 shadow-sm">
		<h3 class="text-lg font-semibold text-slate-800 mb-2">Welcome to StockFlow</h3>
		<p class="text-slate-600">
			This is the main dashboard area. The sidebar and header are provided by the global layout.
		</p>
		<div class="mt-4 flex gap-2">
			<Button variant="outline">Secondary</Button>
			<Button variant="destructive">Delete</Button>
		</div>
	</div>
</div>
