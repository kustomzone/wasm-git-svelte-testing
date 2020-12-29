<script>
console.log("hello");
// Tries to load http://localhost:5000/e93399eed71517e6.wasm
// See: https://github.com/petersalomonsen/wasm-git/issues/17#issuecomment-751503414
// import clock_gettime from "wasm-git/lg2.wasm" 

// test();

// async function test() {
// 	console.log("clock_gettime()");
// 	console.dir(await clock_gettime());
// }


// import Module from "wasm-git/lg2.js" // Contains no exports so I just get an empty object


// Module.onRuntimeInitialized = () => {
// 	alert('onRuntimeInitialized')
//     const lg = Module;
// 	console.log("onRuntimeInitialized() lg:");
// 	console.dir(lg);
// }

setTimeout(() => {
	console.log("timer1");
	test();
}, 100);

$: libgitReady = window.ready
$: console.log("libgitReady: ", libgitReady);

async function test() {
	console.log('test() window.ready:', window.ready);
	// setTimeout(() => {
	// 	console.log("timer");
	// }, 10000);

	// console.log("stackAlloc");
	// console.dir(stackAlloc);
	// let result = stackAlloc(100);
	// lg = await Module;

	// console.log("lg");
	// console.dir(lg);
	// lg.callMain(['clone',`http://localhost:5000/test.git`, 'testrepo']);

	// let result = lg.stackAlloc(100);

	const lg = window.lg2;
    const FS = lg.FS;
    // const NODEFS = FS.filesystems.NODEFS;
    const APPFS = FS.filesystems.MEMFS;
	console.log("APPFS");
    FS.mkdir('/working');
	console.log("mkdir");
    FS.mount(APPFS, { root: '.' }, '/working');
	console.log("mount");
    FS.chdir('/working');    
	console.log("chdir");

    FS.writeFile('/home/web_user/.gitconfig', '[user]\n' +
                'name = Test User\n' +
                'email = test@example.com');
	console.log("writeFile()");
    
    // clone a repository from github
    lg.callMain(['clone','https://cors.isomorphic-git.org/github.com/torch2424/made-with-webassembly.git','clonedtest']);
    // lg.callMain(['clone','http://localhost:3000/gitlab.com/saeedareffard1377666/testproject2.git','clonedtest']);
	console.log("clone()");
    
    FS.chdir('clonedtest');
    console.log(FS.readdir('.'));
    lg.callMain(['log']);
}

// lg.onRuntimeInitialized = () => {
//     const FS = lg.FS;
//     const NODEFS = FS.filesystems.NODEFS;

//     FS.mkdir('/working');
//     FS.mount(NODEFS, { root: '.' }, '/working');
//     FS.chdir('/working');    

//     FS.writeFile('/home/web_user/.gitconfig', '[user]\n' +
//                 'name = Test User\n' +
//                 'email = test@example.com');
    
//     // clone a repository from github
//     lg.callMain(['clone','https://github.com/torch2424/made-with-webassembly.git','clonedtest']);
    
//     FS.chdir('clonedtest');
//     console.log(FS.readdir('.'));
//     lg.callMain(['log']);
// };

export let greet;
</script>

<main>
	<h1>{greet}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<div>
	<button  type="button" on:click={() => { alert('TODO - button action'); }}>Test</button>
</div>
