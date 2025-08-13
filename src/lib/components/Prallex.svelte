<script lang="ts">


	const projects = [
		{
			id: 1,
			name: 'Shriresume',
			backgroundImage: 'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaD_OXLh8WN-LVkLX_Brownvase_1.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'download.png',
			link: 'https://shriresume.com/'
		},
		{
			id: 2,
			name: 'Shrivivah',
			backgroundImage: 'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaC9e-ydWJ-7kSdTn_pool_image-9.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'shrivivah_bg.png',
			link: 'https://srivivah.com/'
		},
		{
			id: 3,
			name: 'MCIL Society One',
			backgroundImage: 'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaC9OFSdWJ-7kSdJK_sc-image-9.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'mcilsocietyone.png',
			link: 'https://mcilsocietyone.com/'
		}
	];

</script>

<div  class="relative min-h-screen w-full" id="projects">
	<!-- Parallax Sections -->
	<div class="w-full">
		{#each projects as project}
			<div
				class="project-section relative flex h-screen w-full items-center justify-center overflow-hidden"
				data-id={project.id}
			>
				<div
					class="absolute inset-0 bg-cover bg-fixed bg-center"
					style={`background-image: url(${project.backgroundImage});`}
				></div>
			</div>
		{/each}
	</div>

	<!-- Dark overlay -->
	<div class="absolute inset-0 h-full w-full bg-black/70"></div>
</div>
