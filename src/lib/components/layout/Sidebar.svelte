<script lang="ts">
	import { page } from '$app/state';
	import {
		Activity,
		ChevronDown,
		ChevronRight,
    SquareKanban,
		Group,
		Monitor,
		PanelLeftClose,
		PanelLeftOpen
	} from '@lucide/svelte';
	import type { Component } from 'svelte';

	let collapsed = $state(false);
	let expanded = $state<Set<string>>(new Set(['Projects']));

	function toggle() {
		collapsed = !collapsed;
	}

	function toggleSubmenu(label: string) {
		const next = new Set(expanded);
		if (next.has(label)) {
			next.delete(label);
		} else {
			next.add(label);
		}
		expanded = next;
	}

	type MenuItem = {
		label: string;
		href: string;
		icon?: Component;
		children?: { label: string; href: string; icon?: Component }[];
	};

	const menuItems: MenuItem[] = [
		{ label: 'Dashboard', href: '/dashboard/overview', icon: Monitor },
		{ label: 'Projects', href: '/projects/overview', icon: SquareKanban,
			children: [
				{ label: 'Project Collection', href: '/projects/projectcollection', icon: Group }
			]
		}
	];

	function isActive(href: string): boolean {
		return page.url.pathname === href || page.url.pathname.startsWith(href + '/');
	}
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
			{#if collapsed || !item.children}
				<a
					href={item.href}
					class="flex items-center rounded-md py-2 text-sm font-medium transition-colors
						{collapsed ? 'justify-center px-2' : 'gap-2 px-3'}
						{isActive(item.href)
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
			{:else}
				<div class="space-y-1">
					<button
						onclick={() => toggleSubmenu(item.label)}
						class="w-full flex items-center gap-2 rounded-md px-3 py-2 text-sm font-medium transition-colors
							{isActive(item.href)
								? 'bg-slate-800 text-white'
								: 'text-slate-300 hover:bg-slate-800 hover:text-white'}"
					>
						{#if item.icon}
							<item.icon class="size-5 shrink-0" />
						{/if}
						<span class="flex-1 text-left whitespace-nowrap overflow-hidden">{item.label}</span>
						{#if expanded.has(item.label)}
							<ChevronDown class="size-4 shrink-0" />
						{:else}
							<ChevronRight class="size-4 shrink-0" />
						{/if}
					</button>

					{#if expanded.has(item.label)}
						<div class="ml-6 space-y-1">
							{#each item.children as child}
								<a
									href={child.href}
									class="flex items-center gap-2 rounded-md px-3 py-2 text-sm font-medium transition-colors
										{page.url.pathname === child.href
											? 'bg-slate-800 text-white'
											: 'text-slate-400 hover:bg-slate-800 hover:text-white'}"
								>
									{#if child.icon}
										<child.icon class="size-4 shrink-0" />
									{/if}
									<span class="whitespace-nowrap overflow-hidden">{child.label}</span>
								</a>
							{/each}
						</div>
					{/if}
				</div>
			{/if}
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
