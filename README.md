# Whiteboard App

## Introduction

This version of Whiteboard offers a simple implementation of collaborative drawing. Unlike [Ploma](https://croquet.io/ploma), this whiteboard does not implement a local (speculative) drawing nor curve smoothing.

## Code Organization

`whiteboard.js` is the core of the application. Notice that it has some logic to load old persistent data from a previous implementaion.

## Invoking Whilteboard

While running the whiteboard app does not require Node or Npm; having them installed on your computer in general helps.

First, you need to copy or install two library files. If you already have Node.js and Npm installed, you can run:

   ```bash
   npm run setup
   ```

to download following two files. If your system does not have curl, you can open the unpkg URLs specified below in a web browser, and save the js files under the specified names.

If you don't have npm, manually copy three files.

1. Download croquet.min.js

   ```bash
   curl -L -o croquet/croquet.min.js https://unpkg.com/@croquet/croquet
   ```

2. Download croquet-virtual-dom.js

   ```bash
   curl -L -o croquet/croquet-virtual-dom.js https://unpkg.com/@croquet/virtual-dom
   ```

Those files are downloaded to your local disk to allow local development described below.

3. Add your Croquet API key to `apiKey.js`
   Obtain your apiKey from [Croquet Dev Portal](croquet.io/keys), create `apiKey.js` by copying `apiKey.js-example` to `apiKey.js`, and insert the key into it.

   ```JavaScript
   const apiKey = "<insert your apiKey from croquet.io/keys>";
   export default apiKey;
   ```

4. If you have node installed you can use the simple server implementation:

   ```Bash
   node server.js
   ```

Otherwise, use your own server for local development, or upload the directory to a server. 

## Development and Debugging

Developing whiteboard does not involve any build or transpilation process. Just edit the file and reload the page. All Croquet Virtual DOM applications work this way.

Adjusting CSS or view side event handling can involve a lot of iterative development. To speed up browser reloads, you can add `?isLocal` to the URL (i.e., `localhost:8000/?isLocal`) to skip the actual Croquet network initialization. This flag uses an emulated reflector for a single node impelemented in the Virtual DOM Framework. In other words, you can develop the "single user" aspects of the whiteboard app totally offline in this way.

### Debugging

You can set a breakpoint in code to see what the application is doing. You can certainly insert the `debugger` statement in a JS file. Note, however, that the expander code (most of .js files in the `/src/` directory) are stringified and then evaluated at runtime. It means that the file you navigate to from the Sources tab of the Chrome Development Tool is not the actual code that the browser is running. If you would like to set a break point in a running code, see the source file display in the console:

<p align="center">
<img src="https://gist.githubusercontent.com/yoshikiohshima/6644ea9a84561d6f8ec365003a9ce22a/raw/de5c60ff73262b99ba366d32ca440aa46fb2d1f5/debug.png" width="300"/>
</p>

where in this example showing file as `VM197`, `VM348`, etc. and click on it. Then the expander code that produced the console log can be accessed, and you can insert a break point.
