# Builds/WebGL

This folder is the static-site root for the free iPhone test build. It is not the shipping game. The shipping target is the native iOS player.

A licensed Unity editor fills this folder when you run **PULSE//BREAKERS → Build WebGL (iPhone test)** or:

```
Unity -batchmode -nographics -quit -executeMethod BuildScripts.BuildWebGL
```

`BuildScripts.BuildWebGL` also accepts `-customBuildPath`, which is what the GitHub Action passes. After a successful build the folder looks like this:

```
Builds/WebGL/
  index.html          custom Safari template, processed by Unity
  Build/              .unityweb data, framework, wasm, loader
  .nojekyll           stops GitHub Pages from dropping files that start with _
  HOSTING.txt         short host notes, rewritten by the build
  README.md           this file
```

Open `index.html` over **http or https**. A `file://` URL will not load the player. GitHub Pages: set the site source to GitHub Actions and run the **WebGL** workflow with **Deploy to GitHub Pages** checked. Any other static host can serve this folder as the site root. Paths inside the page are relative (`Build/...`), so a project-site subpath works as long as this folder is the site root.

Compression is Brotli with Unity's decompression fallback, so the host does not need `Content-Encoding: br`. WebAssembly threads are off, because GitHub Pages cannot send the cross-origin isolation headers those threads need.

There is no player in git yet. This machine has no Unity editor and no Unity license, so a fake `Build/` was not committed.
