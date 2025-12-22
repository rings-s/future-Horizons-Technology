<script>
	import { onMount } from 'svelte';
	import { MapPin, Phone, Mail, MessageCircle } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	let isVisible = $state(false);
	let sectionRef;

	onMount(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					isVisible = true;
				}
			},
			{ threshold: 0.1 }
		);

		if (sectionRef) {
			observer.observe(sectionRef);
		}

		return () => observer.disconnect();
	});
</script>

<section
	bind:this={sectionRef}
	id="contact"
	class="relative py-24 lg:py-32 bg-background overflow-hidden"
>
	<!-- Background Gradients -->
	<div
		class="absolute top-0 right-0 w-[800px] h-[800px] bg-primary/5 rounded-full blur-[120px] translate-x-1/3 -translate-y-1/3"
	></div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<div class="grid lg:grid-cols-2 gap-16 lg:gap-24">
			<!-- Contact Info -->
			<div class="space-y-12">
				<div
					class="transition-all duration-700 {isVisible
						? 'opacity-100 translate-x-0'
						: 'opacity-0 -translate-x-12'}"
				>
					<div
						class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6"
					>
						{$t('contact.badge')}
					</div>
					<h2 class="text-4xl sm:text-5xl font-bold text-foreground mb-6 text-balance">
						{$t('contact.title')}
						<span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-blue-500"
							>{$t('contact.titleHighlight')}</span
						>
					</h2>
					<p class="text-xl text-muted-foreground leading-relaxed">
						{$t('contact.subtitle')}
					</p>
				</div>

				<div
					class="space-y-8 transition-all duration-700 delay-200 {isVisible
						? 'opacity-100 translate-x-0'
						: 'opacity-0 -translate-x-12'}"
				>
					<div
						class="group flex items-start gap-6 p-6 rounded-2xl glass border border-white/5 hover:border-primary/20 transition-all duration-300 hover:-translate-y-1"
					>
						<div
							class="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center shrink-0 group-hover:bg-primary group-hover:text-white transition-all duration-300"
						>
							<MapPin class="w-6 h-6" />
						</div>
						<div>
							<h3 class="text-lg font-bold text-foreground mb-1">{$t('contact.headquarters')}</h3>
							<p class="text-muted-foreground">{$t('contact.location')}</p>
						</div>
					</div>

					<div
						class="group flex items-start gap-6 p-6 rounded-2xl glass border border-white/5 hover:border-primary/20 transition-all duration-300 hover:-translate-y-1"
					>
						<div
							class="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center shrink-0 group-hover:bg-primary group-hover:text-white transition-all duration-300"
						>
							<Phone class="w-6 h-6" />
						</div>
						<div>
							<h3 class="text-lg font-bold text-foreground mb-1">{$t('contact.phone')}</h3>
							<p class="text-muted-foreground">{$t('contact.phoneNumber')}</p>
						</div>
					</div>

					<div
						class="group flex items-start gap-6 p-6 rounded-2xl glass border border-white/5 hover:border-primary/20 transition-all duration-300 hover:-translate-y-1"
					>
						<div
							class="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center shrink-0 group-hover:bg-primary group-hover:text-white transition-all duration-300"
						>
							<Mail class="w-6 h-6" />
						</div>
						<div>
							<h3 class="text-lg font-bold text-foreground mb-1">{$t('contact.email')}</h3>
							<p class="text-muted-foreground">{$t('contact.emailAddress')}</p>
						</div>
					</div>
				</div>
			</div>

			<div
				class="transition-all duration-700 delay-300 {isVisible
					? 'opacity-100 translate-x-0'
					: 'opacity-0 translate-x-12'}"
			>
				<div
					class="bg-card/50 backdrop-blur-xl rounded-[2.5rem] border border-white/10 p-8 lg:p-12 shadow-2xl h-full flex flex-col items-center justify-center text-center"
				>
					<div
						class="w-24 h-24 rounded-full bg-[#25D366]/10 flex items-center justify-center mb-6 animate-pulse"
					>
						<MessageCircle class="w-12 h-12 text-[#25D366]" />
					</div>

					<h3 class="text-2xl font-bold text-foreground mb-4">{$t('contact.whatsappTitle')}</h3>
					<p class="text-muted-foreground mb-8 max-w-sm">
						{$t('contact.whatsappSubtitle')}
					</p>

					<!-- TODO: Add WhatsApp number below -->
					<a
						href="https://wa.me/"
						target="_blank"
						rel="noopener noreferrer"
						class="w-full bg-[#25D366] hover:bg-[#128C7E] text-white px-8 py-4 rounded-2xl font-bold text-lg inline-flex items-center justify-center gap-3 transition-all hover:scale-[1.02] shadow-lg shadow-[#25D366]/25"
					>
						<MessageCircle class="w-6 h-6" />
						{$t('contact.whatsappButton')}
					</a>
				</div>
			</div>
		</div>
	</div>
</section>
