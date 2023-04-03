<script lang="ts">
	import { tick } from 'svelte';
	const keymap = {
		f: 'e',
		p: 'r',
		g: 't',
		j: 'y',
		l: 'u',
		u: 'i',
		y: 'o',
		';': 'p',
		r: 's',
		s: 'd',
		t: 'f',
		d: 'g',
		n: 'j',
		e: 'k',
		i: 'l',
		o: ';',
		k: 'n'
	};
	const whitespace = [
		' ',
		'Tab',
		'Enter',
		'Backspace',
		'Delete',
		'ArrowLeft',
		'ArrowRight',
		'ArrowUp',
		'ArrowDown'
	];
	let value = '';

	async function handleKeydown(event: KeyboardEvent) {
		const target = event.target as HTMLTextAreaElement;
		if (
			whitespace.includes(event.key) ||
			event.altKey ||
			event.ctrlKey ||
			event.metaKey ||
			event.shiftKey
		)
			return;
		event.preventDefault();

		const translatedKey = keymap[event.key as keyof typeof keymap] ?? event.key;
		if (translatedKey.length !== 1) return;

		const selectionStart = target.selectionStart;
		value = value.slice(0, selectionStart) + translatedKey + value.slice(selectionStart);
		await tick();
		target.selectionStart = selectionStart + 1;
		target.selectionEnd = selectionStart + 1;
	}
</script>

<hgroup>
	<h1>colemak2qwerty</h1>
	<h2>
		Text you enter here with the Colemak keyboard will be treated as if you are using a QWERTY
		keyboard
	</h2>
</hgroup>

<article>
	<label>
		Enter any text:
		<textarea bind:value on:keydown={handleKeydown} />
	</label>
</article>
