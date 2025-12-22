<script>
	import { Menu, X, ArrowRight, Languages } from 'lucide-svelte';
	import logo from '$lib/assets/logo.svg';
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { locale, t } from 'svelte-i18n';

	const navLinks = [
		{ href: '#about', label: 'nav.about' },
		{ href: '#services', label: 'nav.services' },
		{ href: '#products', label: 'nav.products' },
		{ href: '#values', label: 'nav.values' },
		{ href: '#clients', label: 'nav.clients' },
		{ href: '#contact', label: 'nav.contact' }
	];

	let mobileMenuOpen = $state(false);
	let scrollY = $state(0);
	let isScrolled = $derived(scrollY > 20);

	function toggleMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}

	function switchLanguage() {
		locale.set($locale === 'en' ? 'ar' : 'en');
	}
</script>

<svelte:window bind:scrollY />

<header
	class="fixed top-0 left-0 right-0 z-50 transition-all duration-500 {isScrolled
		? 'bg-background/80 backdrop-blur-xl border-b border-white/10 shadow-lg shadow-black/5 py-2'
		: 'bg-transparent py-4'}"
>
	<div class="container mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex items-center justify-between h-16">
			<!-- Logo -->
			<a href="/" class="group flex items-center gap-3 relative z-50">
				<div
					class="w-12 h-12 rounded-xl bg-white/5 flex items-center justify-center p-1.5 transition-transform duration-300 group-hover:scale-110 group-hover:rotate-3 overflow-hidden"
				>
					<img src={logo} alt="Future Horizons Technology Logo" class="w-full h-full object-contain" />
				</div>
				<div class="hidden sm:block">
					<span
						class="text-lg font-bold text-foreground tracking-tight group-hover:text-primary transition-colors"
						>Future Horizons</span
					>
					<span class="block text-[10px] uppercase tracking-widest text-muted-foreground -mt-1"
						>Technology</span
					>
				</div>
			</a>

			<!-- Desktop Navigation -->
			<nav class="hidden lg:flex items-center gap-1">
				{#each navLinks as link}
					<a
						href={link.href}
						class="relative px-4 py-2 text-sm font-medium text-muted-foreground hover:text-foreground transition-colors group"
					>
						{$t(link.label)}
						<span
							class="absolute inset-x-4 bottom-0 h-px bg-primary scale-x-0 group-hover:scale-x-100 transition-transform duration-300 origin-left"
						></span>
					</a>
				{/each}
			</nav>

			<!-- Language Switcher & CTA -->
			<div class="hidden lg:flex items-center gap-4">
				<div class="flex items-center gap-3" dir="ltr">
					<button
						onclick={() => locale.set('en')}
						class="text-sm font-medium transition-colors {$locale === 'en'
							? 'text-primary'
							: 'text-muted-foreground'}"
					>
						EN
					</button>
					<button
						onclick={switchLanguage}
						class="relative w-14 h-7 bg-secondary/50 rounded-full transition-all duration-300 hover:bg-secondary border border-white/10"
						aria-label="Switch language"
					>
						<div
							class="absolute top-0.5 {$locale === 'en'
								? 'left-0.5'
								: 'left-[26px]'} w-6 h-6 bg-gradient-to-br from-primary to-blue-600 rounded-full shadow-lg transition-all duration-300 flex items-center justify-center"
						>
							<Languages class="w-3 h-3 text-white" />
						</div>
					</button>
					<button
						onclick={() => locale.set('ar')}
						class="text-sm font-medium transition-colors {$locale === 'ar'
							? 'text-primary'
							: 'text-muted-foreground'}"
					>
						ع
					</button>
				</div>

				<button
					class="group relative px-6 py-2.5 bg-primary text-primary-foreground rounded-xl overflow-hidden transition-all hover:shadow-lg hover:shadow-primary/25 hover:-translate-y-0.5"
				>
					<div
						class="absolute inset-0 bg-gradient-to-r from-transparent via-white/20 to-transparent translate-x-[-200%] group-hover:animate-shimmer"
					></div>
					<span class="relative flex items-center gap-2 text-sm font-semibold">
						{$t('nav.getQuote')}
						<ArrowRight class="w-4 h-4 group-hover:translate-x-1 transition-transform" />
					</span>
				</button>
			</div>

			<!-- Mobile Menu Button -->
			<button
				class="lg:hidden relative z-50 p-2 text-foreground hover:bg-white/5 rounded-lg transition-colors"
				onclick={toggleMenu}
				aria-label="Toggle menu"
			>
				{#if mobileMenuOpen}
					<X class="w-6 h-6" />
				{:else}
					<Menu class="w-6 h-6" />
				{/if}
			</button>
		</div>
	</div>

	<!-- Mobile Navigation Overlay -->
	{#if mobileMenuOpen}
		<div
			class="fixed inset-0 bg-background/95 backdrop-blur-2xl z-40 lg:hidden flex flex-col pt-24 px-6"
			transition:fade={{ duration: 200 }}
		>
			<nav class="flex flex-col gap-2">
				{#each navLinks as link, i}
					<a
						href={link.href}
						class="text-2xl font-medium text-foreground/80 hover:text-primary py-3 border-b border-white/5 transition-colors flex items-center justify-between group"
						onclick={() => (mobileMenuOpen = false)}
						in:slide={{ delay: i * 50, duration: 300 }}
					>
						{$t(link.label)}
						<ArrowRight
							class="w-5 h-5 opacity-0 -translate-x-4 group-hover:opacity-100 group-hover:translate-x-0 transition-all"
						/>
					</a>
				{/each}

				<button
					onclick={switchLanguage}
					class="flex items-center gap-3 text-2xl font-medium text-foreground/80 hover:text-primary py-3 border-b border-white/5 transition-colors"
					in:slide={{ delay: navLinks.length * 50, duration: 300 }}
				>
					<Languages class="w-6 h-6" />
					{$locale === 'en' ? 'العربية' : 'English'}
				</button>

				<button
					class="w-full mt-8 bg-primary text-primary-foreground py-4 rounded-xl font-semibold text-lg hover:bg-primary/90 transition-colors flex items-center justify-center gap-2"
					in:slide={{ delay: (navLinks.length + 1) * 50, duration: 300 }}
				>
					{$t('nav.getQuote')}
					<ArrowRight class="w-5 h-5" />
				</button>
			</nav>
		</div>
	{/if}
</header>

<style>
	@keyframes shimmer {
		100% {
			transform: translateX(200%);
		}
	}

	:global(.animate-shimmer) {
		animation: shimmer 2s infinite;
	}
</style>
