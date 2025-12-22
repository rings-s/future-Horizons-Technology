<script>
	import { Facebook, Twitter, Instagram, Linkedin, ArrowRight } from 'lucide-svelte';
	import logo from '$lib/assets/logo.svg';
	import { t } from 'svelte-i18n';

	const footerLinks = {
		services: [
			{ labelKey: 'footer.salesRental', href: '#services' },
			{ labelKey: 'footer.maintenance', href: '#services' },
			{ labelKey: 'footer.spareParts', href: '#products' },
			{ labelKey: 'footer.technicalSupport', href: '#services' }
		],
		company: [
			{ labelKey: 'footer.aboutUs', href: '#about' },
			{ labelKey: 'footer.ourValues', href: '#values' },
			{ labelKey: 'footer.clients', href: '#clients' },
			{ labelKey: 'footer.contact', href: '#contact' }
		],
		products: [
			{ labelKey: 'footer.copiers', href: '#products' },
			{ labelKey: 'footer.inks', href: '#products' },
			{ labelKey: 'footer.spareParts', href: '#products' },
			{ labelKey: 'footer.accessories', href: '#products' }
		]
	};

	const currentYear = new Date().getFullYear();
</script>

<footer class="bg-background border-t border-white/5 relative overflow-hidden">
	<!-- Background Elements -->
	<div class="absolute inset-0 bg-gradient-to-b from-background to-black/50"></div>
	<div
		class="absolute top-0 left-1/2 -translate-x-1/2 w-full max-w-7xl h-px bg-gradient-to-r from-transparent via-primary/50 to-transparent"
	></div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 py-20 relative z-10">
		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-12 gap-12 lg:gap-8 mb-16">
			<!-- Brand -->
			<div class="lg:col-span-4 space-y-6">
				<a href="/" class="flex items-center gap-3 group">
					<div
						class="w-12 h-12 rounded-xl bg-white/5 flex items-center justify-center p-1.5 transition-transform duration-300 group-hover:scale-110 overflow-hidden"
					>
						<img src={logo} alt="Future Horizons Technology Logo" class="w-full h-full object-contain" />
					</div>
					<div>
						<span class="text-xl font-bold text-foreground tracking-tight">Future Horizons</span>
						<span class="block text-[10px] uppercase tracking-widest text-muted-foreground -mt-1"
							>Technology</span
						>
					</div>
				</a>
				<p class="text-muted-foreground leading-relaxed max-w-sm">
					{$t('footer.tagline')}
				</p>
				<div class="flex items-center gap-4">
					{#each [Facebook, Twitter, Instagram, Linkedin] as Icon}
						<a
							href="/"
							class="w-10 h-10 rounded-full glass border border-white/5 flex items-center justify-center text-muted-foreground hover:text-primary hover:bg-primary/10 transition-all hover:-translate-y-1"
						>
							<Icon class="w-5 h-5" />
						</a>
					{/each}
				</div>
			</div>

			<!-- Links -->
			<div class="lg:col-span-2 lg:col-start-6">
				<h3 class="text-sm font-bold text-foreground uppercase tracking-widest mb-6">
					{$t('footer.services')}
				</h3>
				<ul class="space-y-4">
					{#each footerLinks.services as link}
						<li>
							<a
								href={link.href}
								class="text-muted-foreground hover:text-primary transition-colors text-sm flex items-center gap-2 group"
							>
								<ArrowRight
									class="w-3 h-3 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all"
								/>
								{$t(link.labelKey)}
							</a>
						</li>
					{/each}
				</ul>
			</div>

			<div class="lg:col-span-2">
				<h3 class="text-sm font-bold text-foreground uppercase tracking-widest mb-6">
					{$t('footer.company')}
				</h3>
				<ul class="space-y-4">
					{#each footerLinks.company as link}
						<li>
							<a
								href={link.href}
								class="text-muted-foreground hover:text-primary transition-colors text-sm flex items-center gap-2 group"
							>
								<ArrowRight
									class="w-3 h-3 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all"
								/>
								{$t(link.labelKey)}
							</a>
						</li>
					{/each}
				</ul>
			</div>

			<div class="lg:col-span-2">
				<h3 class="text-sm font-bold text-foreground uppercase tracking-widest mb-6">
					{$t('footer.products')}
				</h3>
				<ul class="space-y-4">
					{#each footerLinks.products as link}
						<li>
							<a
								href={link.href}
								class="text-muted-foreground hover:text-primary transition-colors text-sm flex items-center gap-2 group"
							>
								<ArrowRight
									class="w-3 h-3 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all"
								/>
								{$t(link.labelKey)}
							</a>
						</li>
					{/each}
				</ul>
			</div>
		</div>

		<!-- Bottom Bar -->
		<div
			class="pt-8 border-t border-white/5 flex flex-col md:flex-row items-center justify-between gap-6"
		>
			<p class="text-sm text-muted-foreground text-center md:text-left">
				© {currentYear}
				{$t('footer.copyright')}
			</p>
			<div class="flex items-center gap-8 text-sm text-muted-foreground">
				<span class="flex items-center gap-2">
					<span class="w-1.5 h-1.5 rounded-full bg-green-500"></span>
					{$t('footer.commercialReg')}
				</span>
				<span>{$t('footer.location')}</span>
			</div>
		</div>
	</div>
</footer>
