<script lang="ts">
	import { Button } from '$lib/components/ui/button/index.js';

	const collections = [
		{ name: 'Growth Portfolio', projects: 12, owner: 'Alice' },
		{ name: 'Dividend Focus', projects: 8, owner: 'Bob' },
		{ name: 'Tech Stocks', projects: 15, owner: 'Charlie' }
	];
</script>

<div class="space-y-6">
	<div class="flex items-center justify-between">
		<h1 class="text-2xl font-bold text-slate-900">Project Collection</h1>
		<Button>New Collection</Button>
	</div>

	<div class="bg-white rounded-lg border border-slate-200 shadow-sm overflow-hidden">
		<table class="w-full text-sm text-left">
			<thead class="bg-slate-50 text-slate-600 font-medium border-b border-slate-200">
				<tr>
					<th class="px-6 py-3">Name</th>
					<th class="px-6 py-3">Projects</th>
					<th class="px-6 py-3">Owner</th>
					<th class="px-6 py-3 text-right">Actions</th>
				</tr>
			</thead>
			<tbody class="divide-y divide-slate-100">
				{#each collections as collection}
					<tr class="hover:bg-slate-50">
						<td class="px-6 py-4 font-medium text-slate-900">{collection.name}</td>
						<td class="px-6 py-4 text-slate-600">{collection.projects}</td>
						<td class="px-6 py-4 text-slate-600">{collection.owner}</td>
						<td class="px-6 py-4 text-right">
							<Button variant="outline" size="sm">View</Button>
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
	</div>
</div>
