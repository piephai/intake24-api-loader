<script lang="ts">
	let foodFileSelect: string = '';
	let fileHandle;

	const getTheFile = async () => {
		const pickerOpts = {
			startIn: 'pictures',
			types: [
				{
					description: 'Images',
					accept: {
						'image/*': ['.png', '.gif', '.jpeg', '.jpg']
					}
				}
			],
			excludeAcceptAllOption: true,
			multiple: false
		};

		// open file picker
		const [fileHandle] = await window.showOpenFilePicker(pickerOpts);
		// get file contents
		const fileData = await fileHandle.getFile();
		return fileData;
	};

	const handleClick = (fileType: string): any => {
		getTheFile().then((data) => {
			fileType = data.name;
		});
	};
</script>

<div class="flex flex-col text-sm mb-2">
	<label for="uploadform" class="mb-2 font-bold text-gray-800">Foods</label>
	<div>
		<input
			readonly
			type="text"
			name="upload-form"
			class="appearance-none shadow-sm border border-gray-200 p-2 focus:outline-none focus:border-gray-500 rounded-lg"
			bind:value={foodFileSelect}
		/>
		<button type="button" on:click={handleClick('foodFileSelect')} class=""> Food Upload </button>
	</div>
</div>
