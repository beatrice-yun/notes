<script>
	import marked from 'marked';

	let source = `
		# H1 Titre

		## H2 Titre

		### H3 Titre

		---

		**Texte en gras**

		*Texte en italique*

		---

		1. 1er choix
		2. 2ème choix
		3. 3ème choix

		- 1er choix
		- 2ème choix
		- 3ème choix
		`;

//	let markdown = marked(source);
	$: markdown = marked(source);

  function toggleOuput() {
    // get the output
    var theOutput = document.getElementById('outputContainer');

    // get the current value of the output's display property
    var displaySetting = theOutput.style.display;

    // also get the output button, so we can change what it says
    var clockButton = document.getElementById('outputButton');

    // now toggle the output and the button text, depending on current state
    if (displaySetting == 'block') {
      // output is hidden. show it
      theOutput.style.display = 'none';
      // change button text
      outputButton.innerHTML = 'Montrer le résultat';
    }
    else {
      // output is showing. hide it
      theOutput.style.display = 'block';
      // change button text
      outputButton.innerHTML = 'Masquer le résultat';
    }
	}

</script>

<main class="container">
	<header class="header">
			<h1 class="header-title">Notes</h1>
	</header>

	<div id="hide-show-btn">
		<button on:click={toggleOuput} id="outputButton">Montrer le résultat</button>
	</div>

	<div class="markdown-editor">
			<div class="left-panel">
					<textarea bind:value={source} class="source"></textarea>
			</div>
			
			<div id="outputContainer" class="right-panel">
					<div class="output">{@html markdown}<div>
			</div>
	</div>
</main>

<style>

	.container{
        background: #ffffff;
        padding:10px 30px;
    }

    .header {
        height: 10vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .header-title {
        margin: 0;
        color:#FF1D15;
    }

    .markdown-editor {
        width: 100%;
        display: flex;
        align-items:flex-start;
        justify-content: space-evenly;
    }

    .left-panel, .right-panel {
        width: 50%;
        border: solid 1px #001628;
        height: 85vh;
        background: #ffffff;
    }

    .right-panel {
        overflow: auto;
    }

    .source {
        border: none;
        width: 100%;
        height: 100%;
        background: #FFFC31;
        color: #001628;
    }

    .source:focus {
        outline: none;
    }

    .output {
        width: 100%;
        padding: 0 2em;
    }

		#hide-show-btn {
        margin: 20px; 
				display:flex;
        justify-content: center;
    }

    #outputButton {
        color: #001628;
        border: solid 1px #001628;
        box-shadow: 6px 6px 0px #001628;
    }
    
    #outputContainer {
        display: none;
    }

</style>