<script>
	import {tick} from 'svelte';
	import {saveSelection, restoreSelection} from './selection.js'

	let inputbox, html = '', password;

	function clearInput(e) {
		inputbox.innerHTML = '';
	}

	function handleInput(e) {
		const savedSelection = saveSelection(inputbox);
		html = Array.from(e.target.textContent)
			.map((char, i) => ('<span class="' + (password[i] === char ? 'correct' : 'incorrect') + '">' + char + '</span>'))
			.join('');
		tick().then(() => { 
			restoreSelection(inputbox, savedSelection);
		})
	}
</script>

<input id="passwordbox" type="text" spellcheck="false" bind:value={password} on:input={clearInput} />
<div contenteditable="true" id="inputbox" spellcheck="false" bind:this={inputbox} on:input={handleInput}>{@html html}</div>