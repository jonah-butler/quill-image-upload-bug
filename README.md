# quill-example
```
A sample vue3 project showing a formatting bug when using a custom image handler to insert a new image url into the Quill editor.
```

## Steps to Reproduce bug
```
> Clone project
> run npm install
> run npm run serve
> Navigate to /
> In the editor, select the image upload icon in the toolbar
> Select any file, it doesn't really matter
> Image handler will insert new image url - simulating the return from an image file uploaded to a server
> Press Enter
> Cursor will jump back to before the image
> It is not possible to use a carriage return when calling insertEmbed on a new image Delta
> If you type a character, the new line is forced, but breaks formatting, as that text is inside the p tags wrapping the img tag
> To verify this, select the See Contents button
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your unit tests
```
npm run test:unit
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
