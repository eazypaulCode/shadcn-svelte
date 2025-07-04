<svelte:options runes />

<script lang="ts">
	import Announcement from "$lib/components/announcement.svelte";
	import ExamplesNav from "$lib/components/examples-nav.svelte";
	import PageActions from "$lib/components/page-header/page-actions.svelte";
	import PageHeaderDescription from "$lib/components/page-header/page-header-description.svelte";
	import PageHeaderHeading from "$lib/components/page-header/page-header-heading.svelte";
	import PageHeader from "$lib/components/page-header/page-header.svelte";
	import PageNav from "$lib/components/page-nav.svelte";
	import ThemeSelector from "$lib/components/theme-selector.svelte";
	import Button from "$lib/registry/ui/button/button.svelte";
	import CardsDemo from "$lib/components/cards/demo.svelte";
	import Metadata from "$lib/components/metadata.svelte";
	import { IsMobile } from "$lib/registry/hooks/is-mobile.svelte.js";

	const title = "Build your Component Library";
	const description =
		"A set of beautifully-designed, accessible components and a code distribution platform. Open Source. Open Code.";

	const mobile = new IsMobile();
</script>

<Metadata {title} {description} />

<div class="flex flex-1 flex-col">
	<PageHeader>
		<Announcement />
		<PageHeaderHeading>{title}</PageHeaderHeading>
		<PageHeaderDescription>{description}</PageHeaderDescription>
		<PageActions>
			<Button href="/docs/installation" size="sm">Get Started</Button>
			<Button href="/blocks" size="sm" variant="ghost">Browse Blocks</Button>
		</PageActions>
	</PageHeader>
	{#if !mobile.current}
		<PageNav class="hidden md:flex">
			<ExamplesNav class="[&>a:first-child]:text-primary flex-1 overflow-hidden" />
			<ThemeSelector class="mr-4 hidden md:flex" />
		</PageNav>
	{/if}
	<div class="container-wrapper section-soft flex-1 pb-6">
		<div class="container overflow-hidden">
			<section
				class="border-border/50 -mx-4 w-[160vw] overflow-hidden rounded-lg border md:hidden md:w-[150vw]"
			>
				<enhanced:img
					class="block object-cover dark:hidden"
					src="../../../static/img/registry/dashboard-01-light-landing.png?w=716"
					alt="Dashboard"
					fetchpriority={mobile.current ? "high" : undefined}
					loading={mobile.current ? "eager" : "lazy"}
				/>
				<enhanced:img
					class="hidden object-cover dark:block"
					src="../../../static/img/registry/dashboard-01-dark-landing.png?w=716"
					alt="Dashboard"
					fetchpriority="high"
					loading={mobile.current ? "eager" : "lazy"}
				/>
			</section>
			{#if !mobile.current}
				<section class="theme-container hidden md:block">
					<CardsDemo />
				</section>
			{/if}
		</div>
	</div>
</div>
