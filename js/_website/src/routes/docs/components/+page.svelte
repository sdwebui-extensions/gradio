<script lang="ts">
	import DocsNav from "../../../components/DocsNav.svelte";
	import MetaTags from "../../../components/MetaTags.svelte";
	import dataflow_svg from "../../../assets/img/dataflow.svg";

	export let data;

	let components: Record<string, any> = data.components;
	let helpers = data.helpers;
	let routes = data.routes;
	let events = data.events;
	let events_matrix = data.events_matrix;
	let py_client = data.py_client;
</script>

<MetaTags
	title={"Gradio Component Docs"}
	url={"https://gradio.app/docs/components"}
	canonical={"https://gradio.app/docs/components"}
	description={"Gradio includes pre-built components that can be used as inputs or outputs in your Interface or Blocks with a single line of code."}
/>

<main class="container mx-auto px-4 flex gap-4">
	<DocsNav
		current_nav_link={"components"}
		{components}
		{helpers}
		{routes}
		{py_client}
	/>

	<div class="flex flex-col w-full min-w-full lg:w-10/12 lg:min-w-0">
		<div>
			<p
				class="bg-gradient-to-r from-orange-100 to-orange-50 border border-orange-200 px-4 py-1 mr-2 rounded-full text-orange-800 mb-1 w-fit float-left"
			>
				New to Gradio? Start here: <a class="link" href="/quickstart"
					>Getting Started</a
				>
			</p>
			<p
				class="bg-gradient-to-r from-green-100 to-green-50 border border-green-200 px-4 py-1 rounded-full text-green-800 mb-1 w-fit float-left sm:float-right"
			>
				See the <a class="link" href="/changelog">Release History</a>
			</p>
		</div>

		<div class="flex justify-between mt-4">
			<a
				href="/docs/themes"
				class="text-left px-4 py-1 bg-gray-50 rounded-full hover:underline"
			>
				<div class="text-lg">
					<span class="text-orange-500">&#8592;</span> Themes
				</div>
			</a>
			<a
				href="/docs/audio"
				class="text-right px-4 py-1 bg-gray-50 rounded-full hover:underline"
			>
				<div class="text-lg">
					Audio <span class="text-orange-500">&#8594;</span>
				</div>
			</a>
		</div>
		<div class="flex flex-row">
			<div class="lg:w-3/4 lg:ml-10 lg:mr-24">
				<div class="obj" id="components">
					<h2
						id="components-header"
						class="text-4xl font-light mb-2 pt-2 text-orange-500"
					>
						Components
					</h2>

					<p class="mt-8 mb-2 text-lg">
						Gradio includes pre-built components that can be used as inputs or
						outputs in your Interface or Blocks with a single line of code.
						Components include <em>preprocessing</em> steps that convert user
						data submitted through browser to something that be can used by a
						Python function, and <em>postprocessing</em>
						steps to convert values returned by a Python function into something
						that can be displayed in a browser.
					</p>

					<p class="mt-2 text-lg">
						Consider an example with three inputs &lpar;Textbox, Number, and
						Image&rpar; and two outputs &lpar;Number and Gallery&rpar;, below is
						a diagram of what our preprocessing will send to the function and
						what our postprocessing will require from it.
					</p>

					<img src={dataflow_svg} class="mt-4" />

					<p class="mt-2 text-lg">
						Components also come with certain events that they support. These
						are methods that are triggered with user actions. Below is a table
						showing which events are supported for each component. All events
						are also listed &lpar;with parameters&rpar; in the component's docs.
					</p>
				</div>

				<div class="max-h-96 overflow-y-scroll my-6">
					<table class="table-fixed leading-loose">
						<thead class="text-center sticky top-0">
							<tr>
								<th class="p-3 bg-white w-1/5 sticky left-0" />
								{#each events as event}
									<th class="p-3 font-normal bg-white border-t border-l"
										>{event}</th
									>
								{/each}
							</tr>
						</thead>
						<tbody
							class=" rounded-lg bg-gray-50 border border-gray-100 overflow-hidden text-left align-top divide-y"
						>
							{#each Object.entries(components) as [name, obj] (name)}
								<tr class="group hover:bg-gray-200/60">
									<th class="p-3 w-1/5 bg-white sticky z-2 left-0 font-normal">
										<a href={obj.name.toLowerCase()} class="thin-link"
											>{obj.name}</a
										>
									</th>
									{#each events as event}
										<td class="p-3 text-gray-700 break-words text-center">
											{#if events_matrix[obj.name].includes(event.toLowerCase())}
												<p class="text-orange-500">&#10003;</p>
											{:else}
												<p class="text-gray-300">&#10005;</p>
											{/if}
										</td>
									{/each}
								</tr>
							{/each}
						</tbody>
					</table>
				</div>
			</div>
		</div>
		<div class="flex justify-between my-4">
			<a
				href="/docs/block-layouts"
				class="text-left px-4 py-1 bg-gray-50 rounded-full hover:underline"
			>
				<div class="text-lg">
					<span class="text-orange-500">&#8592;</span> Block Layouts
				</div>
			</a>
			<a
				href="/docs/audio"
				class="text-right px-4 py-1 bg-gray-50 rounded-full hover:underline"
			>
				<div class="text-lg">
					Audio <span class="text-orange-500">&#8594;</span>
				</div>
			</a>
		</div>
	</div>
</main>
