<script lang="ts">
	import { page } from '$app/state';
	import { Activity, Monitor } from '@lucide/svelte';
	import type { Component } from 'svelte';

	const menuItems: { label: string; href: string; icon?: Component }[] = [
		{ label: 'Dashboard', href: '/dashboard/overview', icon: Monitor }
	];
</script>

<aside class="w-64 h-screen bg-slate-900 text-slate-100 flex flex-col">
	<div class="h-16 flex items-center px-6 border-b border-slate-800 gap-2">
    <Activity class="size-6 text-green-600" />
		<h1 class="text-xl font-bold tracking-tight">StockFlow</h1>
	</div>

	<nav class="flex-1 py-4 px-3 space-y-1">
		{#each menuItems as item}
			<a
				href={item.href}
				class="flex items-center gap-2 rounded-md px-3 py-2 text-sm font-medium transition-colors
					{page.url.pathname === item.href
						? 'bg-slate-800 text-white'
						: 'text-slate-300 hover:bg-slate-800 hover:text-white'}"
			>
				{#if item.icon}
					<item.icon class="size-4" />
				{/if}
				<span>{item.label}</span>
			</a>
		{/each}
	</nav>

	<div class="p-4 border-t border-slate-800 text-xs text-slate-500">
		StockFlow © 2025
	</div>
</aside>
