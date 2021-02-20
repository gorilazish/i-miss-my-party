<script context="module">
	let current;
</script>

<script>
	export let src
	export let title;
	export let composer;
	export let performer;
	let audio;
	let paused = true;
    let volume = 0
	function stopOthers() {
		// if (current && current !== audio) current.pause();
		// current = audio;
	}
</script>

<style>
	article { margin: 0 0 1em 0; max-width: 800px; color: #c7c2c0; }
	h2, p { margin: 0 0 0.3em 0; }
	audio { width: 100%; margin: 0.5em 0 1em 0; }
    
	.playing { color: #33302f; }

    audio {
        width: 200px;
    }

/* Removes the timeline */
audio::-webkit-media-controls-timeline {
  display: none !important;
}

/* Removes the time stamp */
audio::-webkit-media-controls-current-time-display {
  display: none;
}

audio::-webkit-media-controls-time-remaining-display {
  display: none;
}
</style>

<article class:playing={!paused}>
	<h2>{title}</h2>
    {#if composer}
	    <p><strong>{composer || ''}</strong> / performed by {performer || ''}</p>
    {/if}

	<audio
    autoplay
    controlsList="nodownload"
		bind:this={audio}
		bind:paused
        bind:volume
		on:play={stopOthers}
		controls
		{src}
	></audio>
</article>