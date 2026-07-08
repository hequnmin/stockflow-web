<script lang="ts">
	import { page } from '$app/state';
	import { Activity, Monitor, PanelLeftClose, PanelLeftOpen } from '@lucide/svelte';
	import type { Component } from 'svelte';

	let collapsed = $state(false);

	function toggle() {
		collapsed = !collapsed;
	}

	const menuItems: { label: string; href: string; icon?: Component }[] = [
		{ label: 'Dashboard', href: '/dashboard/overview', icon: Monitor }
	];
</script>

<aside
	class="h-screen bg-slate-900 text-slate-100 flex flex-col transition-all duration-300 ease-in-out {collapsed
		? 'w-16'
		: 'w-64'}"
>
	<div
		class="h-16 flex items-center border-b border-slate-800 gap-2 transition-all duration-300 {collapsed
			? 'justify-center px-2'
			: 'px-6'}"
	>
		<Activity class="size-6 text-green-600 shrink-0" />
		{#if !collapsed}
			<h1 class="text-xl font-bold tracking-tight whitespace-nowrap overflow-hidden">StockFlow</h1>
		{/if}
	</div>

	<nav class="flex-1 py-4 px-3 space-y-1">
		{#each menuItems as item}
			<a
				href={item.href}
				class="flex items-center rounded-md py-2 text-sm font-medium transition-colors
					{collapsed ? 'justify-center px-2' : 'gap-2 px-3'}
					{page.url.pathname === item.href
						? 'bg-slate-800 text-white'
						: 'text-slate-300 hover:bg-slate-800 hover:text-white'}"
			>
				{#if item.icon}
					<item.icon class="size-5 shrink-0" />
				{/if}
				{#if !collapsed}
					<span class="whitespace-nowrap overflow-hidden">{item.label}</span>
				{/if}
			</a>
		{/each}
	</nav>

	<div class="p-4 border-t border-slate-800">
		<button
			onclick={toggle}
			class="w-full flex items-center rounded-md py-2 text-sm font-medium text-slate-300 hover:bg-slate-800 hover:text-white transition-colors {collapsed
				? 'justify-center px-2'
				: 'justify-end px-3'}"
			aria-label={collapsed ? '展开侧边栏' : '收缩侧边栏'}
		>
			{#if collapsed}
				<PanelLeftOpen class="size-5 shrink-0" />
			{:else}
				<PanelLeftClose class="size-5 shrink-0" />
			{/if}
		</button>
	</div>
</aside>
