<script lang="ts">
	import { Button } from '$lib/components/ui/button/index.js';

	const projects = [
		{ name: 'Alpha Strategy', status: 'Active', progress: 72 },
		{ name: 'Beta Portfolio', status: 'Planning', progress: 30 },
		{ name: 'Gamma Watchlist', status: 'Active', progress: 55 }
	];
</script>

<div class="space-y-6">
	<div class="flex items-center justify-between">
		<h1 class="text-2xl font-bold text-slate-900">Projects</h1>
		<Button>New Project</Button>
	</div>

	<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
		{#each projects as project}
			<div class="bg-white rounded-lg border border-slate-200 p-6 shadow-sm space-y-4">
				<div class="flex items-center justify-between">
					<h3 class="text-lg font-semibold text-slate-800">{project.name}</h3>
					<span
						class="text-xs font-medium px-2 py-1 rounded-full {project.status === 'Active'
							? 'bg-green-100 text-green-700'
							: 'bg-amber-100 text-amber-700'}"
					>
						{project.status}
					</span>
				</div>

				<div class="space-y-1">
					<div class="flex justify-between text-sm text-slate-600">
						<span>Progress</span>
						<span>{project.progress}%</span>
					</div>
					<div class="h-2 bg-slate-100 rounded-full overflow-hidden">
						<div
							class="h-full bg-primary transition-all"
							style="width: {project.progress}%"
						></div>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>
