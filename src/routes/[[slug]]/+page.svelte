<script lang="ts">
	import Tablelist from '$lib/components/Tablelist.svelte';
	import TypeSlot from '$lib/components/TypeSlot.svelte';
	import activeFilters, { filters } from '$lib/filter';
	import {
		format,
		missingMaterial,
		translationNone,
		translationPartly,
		unofficial
	} from '$lib/svg';
	import MultiSelect from 'svelte-multiselect';
</script>

<div class="ml-8 mt-2 flex flex-col md:flex-row">
	<div class="md:pr-4">
		<h1 class="text-2xl">All Type-Moon shared universe works, in release order</h1>
		<h2 class="text-xl text-gray-500 dark:text-gray-400">(Not all works are currently present)</h2>
		<br />
		<img
			src="/images/clueless.png"
			alt="hmm today i will download the entirety of the nasuverse seßries and freely distribute it diregarding any and all copyright law. *clueless*"
			class="mb-4 h-60 w-60 md:hidden"
		/>
		<p class="max-w-xl">
			This page consists of a table of all Nasuverse works. You can sort the table by clicking on
			the column headers, filter the entries by release type, and mark rows as complete by clicking
			on the checkbox.
		</p>
		<p class="mt-4 max-w-md">
			If you spot a missing entry or any errors, don't hesitate to contact me on <a
				href="mailto:nasuverse@colorman.me">nasuverse@colorman.me</a
			>.
		</p>
		<p class="ml-2 mt-2 hidden text-sm text-gray-500 dark:text-gray-400 md:block">
			Tip: Ctrl+click on a link to toggle open all rows.
		</p>
		<hr class="my-2 w-full border-slate-500 lg:w-2/3" />
		<ul>
			<li>
				{@html format} - Format should be updated
			</li>
			<li>
				{@html translationNone} - Not translated
			</li>
			<li>
				{@html translationPartly} - Only partly translated
			</li>
			<li>
				{@html missingMaterial} - Missing material. Contact me if you have a source!
			</li>
			<li>
				{@html unofficial} - Unofficial - not published directly by Type-Moon
			</li>
		</ul>
	</div>
	<div>
		<div class="flex flex-col md:flex-row">
			<img
				src="/images/clueless.png"
				alt="hmm today i will download the entirety of the nasuverse series and freely distribute it diregarding any and all copyright law. *clueless*"
				class="hidden h-60 w-60 md:block"
			/>
			<!-- <a
				href="https://thecolorman.github.io/Fate-Timeline/"
				target="_blank"
				rel="noopener noreferrer"
				class="relative ml-4 flex h-52 w-52"
			>
				<div
					class="absolute bottom-0 left-0 right-0 top-0 z-0 bg-[url('/images/timeline.jpg')] bg-cover bg-center"
				/>
				<div
					class="relative flex h-full w-full items-center justify-center bg-gray-300/60 text-gray-800 transition-all hover:bg-gray-500/60 hover:text-white"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="h-14 w-14"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25"
						/>
					</svg>
					<p class="absolute bottom-1 z-10 self-center text-center">View the Nasuverse timeline</p>
				</div>
			</a> -->
		</div>
		<p class="mt-4 max-w-sm">
			<b>Help needed!</b><br />
			A lot of Type-Moon works, especially the older ones, remain missing {@html missingMaterial} or
			untranslated {@html translationPartly}
			{@html translationNone}. If you have any of the missing works, or can help with translations,
			please reach out at
			<a href="mailto:mailto:nasuverse@colorman.me">nasuverse@colorman.me</a>!
		</p>
	</div>
</div>
<div class="mt-8">
	<MultiSelect
		bind:selected={$activeFilters}
		options={filters}
		liSelectedClass="!bg-primary dark:!bg-dark-primary"
		outerDivClass="!border-border dark:!border-dark-border"
		ulOptionsClass="!bg-primary dark:!bg-dark-primary"
		placeholder="Filters"
		let:option
	>
		<TypeSlot {option} />
		<span slot="after-input">
			{`${$activeFilters.length}/${filters.length} filters applied`}
		</span>
	</MultiSelect>
	<Tablelist />
</div>
