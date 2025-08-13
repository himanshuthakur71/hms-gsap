<script lang="ts">
	import { page } from "$app/state";
	import { projects } from "$lib/jsons/projects.json";
	import { error } from "@sveltejs/kit";

  let project = projects.find((p:any) => p.id == page.params.id);

  $effect(() => {
    if(!project?.id) {
        throw error(404, 'not found')
    }
  })
</script>



<section class="w-full pt-[calc(38.4px+72px)]">
    <div class="px-4">
        <div class="w-full flex items-start justify-between">
            <div>
                <a href="/project" class="flex justify-center items-center size-[48px] bg-white rounded-full">
            X
            </a>
            </div>

            <div class="">
                <div>
                    <p>client</p>
                    <p>xxClient Namexx</p>
                </div>
            </div>
        </div>


        <div>
            <h1>xxProjectNamexx</h1>
        </div>

    </div>


    <div class="w-full">
        <figure class=" w-screen flex justify-center items-center h-screen projectImage" data-flip-id="cover-{project?.id}">
            <img src="{project?.projectImage}" alt="peoject_img" class="w-full h-full">
        </figure>
    </div>
</section>