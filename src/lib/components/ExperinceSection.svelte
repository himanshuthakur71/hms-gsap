<section class=" h-full w-full bg-[#f7f3ed] py-32">
	<div class="w-full px-4 grid grid-cols-2">
		<div class="w-full">
			<ul class=" w-full max-w-[355px]">
				{#each Array(4) as _, i}
					<li class=" flex  items-center gap-4  py-2 border-t-[1px] border-[#0000001a]" class:border-b={i == 3}>
						<span class=" flex justify-center items-center size-[25px] bg-[#d5c8b0] text-[11px] rounded-full">{i+1}</span>
                        <span class=" text-[22px] text-[#333335] font-[400]">Lorem ipsum dolor sit.</span>
					</li>
				{/each}
			</ul>
		</div>

        <div class="w-full">
                <p> <span class=" flex justify-center items-center size-[5px]  rounded-full bg-[#9e8f7b]"></span> From idea to impact</p>
        </div>
	</div>
</section>
