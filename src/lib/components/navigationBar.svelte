<script>
	export let currentPath; // This will receive the path from layout

	import { fade } from "svelte/transition";
	import { onMount } from "svelte";
	import { links } from "$lib/utils/links";
	
	import ActionLink from "./actionLink.svelte";
	import MenuButton from "./menuButton.svelte";
	
	let hasBlur = false;
	const handleScroll = () => {
		window.scrollY > 10 ? hasBlur = true : hasBlur = false;
	};
	
	onMount(() => {
		window.addEventListener('scroll', handleScroll);
		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
	
	let isModalOpen = false;
	const toggleModal = () => {
		isModalOpen = !isModalOpen;
		document.body.classList.toggle('-no-scroll', isModalOpen);
	};
	
</script>

<div class:-has-blur={hasBlur} class="navigation_bar -top">
	<div class="container">
		
		<a href="./" aria-label="Homepage">
			<picture>
				<source media="(min-width:650px)" srcset="logotype_w.webp">
				<source media="(min-width:320px)" srcset="logo.webp">
				<img src="logotype_w.webp" alt="Mistaek">
			</picture>
		</a>
		
		<nav>
			<ul class="navigation-links">
				{#each links as link}
				<li>
					<a href={link.url} target={link.isExternal ? "_blank" : ""} rel={link.isExternal ? "noopener noreferrer" : ""} aria-label={link.label} class:active={currentPath === link.url}>
						<p class="body_text -large -subtle navigation_item">{link.label}</p>
					</a>
				</li>
				{/each}
			</ul>
			
			<ActionLink url="https://cal.com/mistaek/15min" customClass="action -outline" label="Book a call" icon="arrow-out" />
			
			{#if !isModalOpen}
			<MenuButton customClass="-outline -compressed" icon="menu" on:toggle={toggleModal} />
			{:else}
			<MenuButton customClass="-outline -compressed" icon="close" on:toggle={toggleModal} />
			{/if}
		</nav>
		
	</div>
</div>

{#if isModalOpen}
<!-- Render your modal with links here -->
<div class="modal -navigation" transition:fade>
	<ul class="navigation-links">
		{#each links as link}
		<li>
			<a href={link.url} target={link.isExternal ? "_blank" : ""} rel={link.isExternal ? "noopener noreferrer" : ""} aria-label={link.label} class:active={currentPath === link.url} on:click={toggleModal}>
				<p class="body_text -large -subtle navigation_item">{link.label}</p>
			</a>
		</li>
		{/each}
	</ul>
</div>
{/if}

<style lang="scss">
	.navigation_bar {
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		z-index: $zindex-fixed;
		
		&.-has-blur {
			-webkit-backdrop-filter: blur(16px);
			backdrop-filter: blur(16px);
			background: rgba(20, 20, 21, .08);
		}
		
		.container {
			max-width: $max-width-container;
			width: 100%;
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: space-between;
			padding: $space-200;
			margin: 0 auto;
			z-index: $zindex-fixed;
			box-sizing: border-box;

			@media(min-width: $breakpoint-xl) {
				& {padding: $space-200 0;}
			}
			
			&::before {
				content: '';
				position: absolute;
				left: 0;
				right: 0;
				bottom: 0;
				width: 80%;
				height: 1px;
				margin: 0 auto;
				background: radial-gradient(62.87% 100% at 50% 100%, $color-brand-dark-lighter 0%, rgba(255, 255, 255, 0) 100%);
			}
			
			a {
				height: auto;
				display: flex;
				flex-direction: row;
				align-items: flex-start;
				color: $color-neutral-100;
				text-decoration: none;

				img { height: $space-500; }
			}
			
			nav {
				display: flex;
				flex-direction: row;
				align-items: center;
				gap: $space-200;
				
				.navigation-links {
					list-style: none;
					display: none;
					align-items: center;
					
					li {
						display: flex;
						margin-left: $space-200;
						
						&:first-child {
							margin-left: 0;
							display: none;
							user-select: none;
							visibility: hidden;
							opacity: 0;
						}
						
						a {
							display: flex;
							flex-direction: row;
							align-items: flex-start;
							color: $color-neutral-100;
							text-decoration: none;
							
							p {
								position: relative;
								white-space: nowrap;
								transition: {
									property: color;
									duration: $transition-duration-fast;
									timing-function: $transition-timing-function;
								}
								
								&::after {
									content: '';
									position:absolute;
									width: 100%;
									height: 1px;
									background-color: $color-neutral-100;
									top: 100%;
									left: 0;
									pointer-events: none;
									transform-origin: 100% 50%;
									transform: scale3d(0, 1, 1);
									transition: transform $transition-duration-fast;
									transition-timing-function: $transition-timing-function;
								}
								
								&:hover {
									color: $color-neutral-100;
									&::after {
										transform-origin: 0% 50%;
										transform: scale3d(1, 1, 1);
									}
								}
							}

							&.active p {
								color: $color-brand-accent;

								&::after {
									transform-origin: 0% 50%;
									transform: scale3d(1, 1, 1);
									background-color: $color-brand-accent;
								}
							}
						}
						
					}
				}
				
				@media(min-width: $breakpoint-xl) {
					& {
						gap: $space-400;
						
						.navigation-links {
							display: flex;
							
							li { margin-left: $space-400;}
						}
					}
				}
			}
			
		}
	}
</style>
