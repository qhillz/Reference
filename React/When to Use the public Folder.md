## When to Use the `public` Folder

Normally we recommend importing [stylesheets](https://create-react-app.dev/docs/adding-a-stylesheet), [images, and fonts](https://create-react-app.dev/docs/adding-images-fonts-and-files) from JavaScript. The `public` folder is useful as a workaround for a number of less common cases:

- You need a file with a specific name in the build output, such as [`manifest.webmanifest`](https://developer.mozilla.org/en-US/docs/Web/Manifest).
- You have thousands of images and need to dynamically reference their paths.
- You want to include a small script like [`pace.js`](https://github.com/CodeByZach/pace) outside of the bundled code.
- Some libraries may be incompatible with webpack and you have no other option but to include it as a `<script>` tag.

Note that if you add a `<script>` that declares global variables, you should read the topic [Using Global Variables](https://create-react-app.dev/docs/using-global-variables) in the next section which explains how to reference them.