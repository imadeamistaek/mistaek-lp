<script>
	import SectionIdentifier from "../components/sectionIdentifier.svelte";	
</script>

<section class="section problem_solution" aria-labelledby="problem-solution-heading">
	<div class="grid">
		
		<div class="content_group">
			
			<SectionIdentifier letter="A" label="The Problem"/>
			
			<header class="heading_group">
				<h4 id="problem_heading">Struggling to turn your vision into a clear, impactful brand?</h4>
				<div class="paragraph_group -vertical">
					<p class="body_text -large -subtle">
						Many startups face the challenge of translating their innovative ideas into a cohesive brand that resonates with their audience.
					</p>
					<p class="body_text -large -subtle">
						Whether it’s ensuring consistency across digital platforms, creating user-friendly designs, or telling a compelling story, the process can feel overwhelming. That's where we come in.
					</p>
				</div>
			</header>
			
		</div>
		
		<div class="content_group">
			
			<SectionIdentifier letter="B" label="Our Unique Solution"/>
			
			<header class="heading_group">
				<h4 id="solution_heading">A streamlined and accessible approach to design</h4>
				<div class="paragraph_group -horizontal">
					<p class="body_text -large -subtle">
						We specialise in creating design systems, UX/UI, product design, branding, and web design that are not just visually stunning but also accessible and easy to understand.
					</p>
					<p class="body_text -large -subtle">
						Our process simplifies the complex, ensuring your brand’s digital presence is cohesive and user-friendly. By embracing mistakes as opportunities for innovation, we turn challenges into solutions that work for you.
					</p>
				</div>
			</header>
			
		</div>
		
	</div>
</section>

<style lang="scss">
	.problem_solution .grid {
		.content_group {
			padding: $space-500 0;
			border-top: $border-width solid $color-brand-dark-lighter;
		}
		
		/* Large screens layout */
		@media(min-width: $breakpoint-lg) {
			& {					
				.content_group {
					grid-column: 1/2;
					grid-row: 1/2;
					
					&:last-child {grid-column: 2/2;grid-row:2/2}
				}
			}
		}
	}
	.problem_solution {padding-top: 0;}
	
</style>