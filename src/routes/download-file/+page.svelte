<script lang="ts">
	let fileNames: string[] = [];

	function handleFileChange(event: Event): void {
		const input = event.target as HTMLInputElement;
		if (!input.files) return; // Ensure `files` exists
		const files: FileList = input.files;
		console.log({ files });
		fileNames = Array.from(files).map((file: File) => file.name); // Extract file names
	}

	function getFileSize(string: string) {
		const [fileName, size, extension] = string.split('.');
		console.log({ fileName, size, extension });
		return size;
	}

	function getFileSizes(size: string) {
		if (Object.keys(fileSizes).includes(size)) {
			return fileSizes[size as keyof typeof fileSizes];
		} else return 'error';
	}

	const fileSizes = {
		'2:3': '4x6, 6x9, 8x12, 21x18, 16x24, 20x30 and 24x36',
		'3:4': '6x8, 9x12, 12x16, 15x20, 18x24',
		'4:5': '4x5, 8x10, 16x20',
		'11:14': '11x114'
	};
</script>

<div class="hide-on-print flex justify-between p-2">
	<div>
		<label>
			Upload files (use filename format, NAME.RATIO:RATIO.png):
			<input type="file" multiple onchange={handleFileChange} />
		</label>
		{#if fileNames.length > 0}
			<h3>Uploaded Files:</h3>
			<ul>
				{#each fileNames as name}
					<!-- {@const size = } -->
					<li>{name}</li>
				{/each}
			</ul>
		{/if}
	</div>

	<div class="">
		<button
			onclick={() => window.print()}
			class="m-1 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
			>Save as PDF</button
		>
		<button
			onclick={() => (fileNames = [])}
			class="m-1 block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
			>Clear</button
		>
	</div>
</div>

<main class="px-2">
	<div class="flex justify-center">
		<img class="max-w-[200px]" src="/logo.png" alt="logo" />
	</div>
	<div class="flex justify-center py-2">
		<h1 class="text-3xl font-bold tracking-tight text-gray-900">
			Thank you so much for your purchase!
		</h1>
	</div>

	<div class="text-md mt-8 space-y-2 text-pretty font-medium text-gray-700 sm:text-xl/8">
		<p>We sincerely hope you enjoy these printable wall art files.</p>

		<p>
			You will find the following digital files in the .zip folder you just downloaded from Etsy
		</p>

		<ul class="">
			{#each fileNames as name}
				<li>{name} ratio file (use to print{getFileSizes(getFileSize(name))})</li>
			{/each}
		</ul>

		<p>Steps to get started</p>
		<ol class="">
			<li>
				1. Open .zip folder and select the file you’d like to use (choose correct ratio size
				depending on what size print you’d like).
			</li>
			<li>
				2. Decide on the printer or printing service you’d like to use. Feel free to print at home
				using a desktop printer or choose a professional print service to order from.
			</li>
			<li>
				3. If printing from a desktop printer from a desktop printer, click on the selected PDF
				document and print the document making sure to match the printer setting to the size of
				paper you are using. If using a video professional print service, place an order using the
				correct file that you selected from the .zip file.
			</li>
		</ol>
		<p class="text-center">Questions? Send an Etsy message or email our support team at</p>
		<p class="text-center">knoxvilleprintables@gmail.com</p>
	</div>
</main>

<style>
	label {
		display: flex;
		flex-direction: column;
		gap: 8px;
	}
</style>
