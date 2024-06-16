---
title: Playground
description: "TinyGo playground. Run Go code directly in the browser and simulate some popular development boards."
---

<link rel="stylesheet" href="/playground/simulator.css">
<link rel="stylesheet" href="/playground/simulator-bootstrap.css">
<script type="module" src="/playground-play.js"></script>
<style>
#playground {
	margin-top: 1.5rem;
	margin-bottom: 0.75rem;
	display: flex;
	flex-direction: column;
}
#playground-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	flex-wrap: wrap;
}
#target .project-name .buttons {
	margin-left: 16px;
}
.playground-editor {
	min-height: 60vh;
	flex: 1 0 0;
	resize: none;
}
.playground-editor:not([style*="height"]) {
	max-height: initial;
}
.playground-editor .cm-scroller {
	flex: 1 0 0;
}
#middle {
	display: flex;
	flex-grow: 1;
	flex-direction: column;
	gap: 0.75rem;
}
#output {
	flex: 1 0 0;
}
@media (min-width: 768px) {
	#playground {
		margin-top: 5rem;
		/* 100% - header - padding bottom */
		height: calc(100vh - 5rem - 0.75rem);
	}
	#middle {
		flex-direction: row;
	}
	.playground-editor {
		min-height: initial;
	}
}
</style>
<div id="playground">
	<div id="playground-header">
		<h2>Playground</h2>
		<div>
			<div id="target" class="btn-group mb-2">
				<button type="button" class="btn btn-primary dropdown-toggle" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
				Console (TinyGo)
				</button>
				<div class="dropdown-menu">
					<a class="dropdown-item active" href>Console (TinyGo)</a>
					<span id="target-loading" class="dropdown-item disabled">Loading...</span>
				</div>
			</div>
			<button type="button" id="btn-flash" class="btn btn-secondary mb-2" disabled>Flash</button>
			<button type="button" id="btn-share" class="btn btn-secondary mb-2">Share</button>
			<button type="button" id="btn-about" class="btn btn-secondary mb-2" data-bs-toggle="modal" data-bs-target="#aboutModal">About</button>
			<a href="/tour/" class="btn btn-secondary mb-2">Tour</a>
		</div>
	</div>
	<div id="middle">
		<div class="playground-editor" tabindex="-1"></div>
		<div id="output" class="simulator inline">{{< readfile "/simulator/simulator.md" >}}</div>
	</div>
	<div class="modal fade" id="aboutModal" tabindex="-1" aria-labelledby="aboutModalTitle" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="exampleModalLabel">About TinyGo Playground</h1>
					<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<p>
						The TinyGo Playground is a service provided by the TinyGo project
						to compile and run small code samples directly in the browser. It
						has been heavily inspired by the <a
						href="https://play.golang.org/">Go Playground</a> but differs in
						some significant ways:
					</p>
					<ul>
						<li>
							We use the <a href="https://github.com/tinygo-org/tinygo">TinyGo compiler</a> in addition to the main Go compiler.
						</li>
						<li>
							Instead of running code on the server, code is compiled to <a
							href="https://webassembly.org/">WebAssembly</a> and runs
							directly in the browser.
						</li>
						<li>
							It can simulate a few popular boards directly in the browser.
							However, please note that this is a simulation which can differ
							in behavior from how the program will run on an actual device.
						</li>
						<li>
							Boards that support drag-and-drop programming can be flashed
							directly using the Flash button.
						</li>
					</ul>
					<p>
						Like the Go Playground, it's possible to share code
						snippets. These code snippets are stored on Google's
						servers in the US and can be viewed by some TinyGo
						members. While we'll try to make sure the shared data
						can only be accessed by those who have the URL, we
						cannot guarantee security. If you accidentally shared
						something that should not be shared (for example, a
						password or personally identifying information), you can
						contact us at
						<a href="mailto:privacy@tinygo.org">privacy@tinygo.org</a>
						with the URL so we can remove it.
					</p>
					<p>
						Source code of the playground: <a
						href="https://github.com/tinygo-org/playground">github.com/tinygo-org/playground</a>.
					</p>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-primary" data-bs-dismiss="modal">Close</button>
				</div>
			</div>
		</div>
	</div>
	<div class="modal modal-lg fade" id="shareModal" tabindex="-1" aria-labelledby="shareModalLabel" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="shareModalLabel">Share</h1>
					<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<div class="input-group">
						<input type="text" class="form-control user-select-all" placeholder="Loading..." readonly/>
						<button class="btn btn-outline-secondary copy-to-clipboard" type="button" data-bs-toggle="tooltip" data-bs-title="Copy to clipboard" data-bs-placement="bottom" disabled><span class="fa fa-clipboard"></span></button>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
