# Vue Image Galery

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

### Lints and fixes files
```
npm run lint
```

### Comments
- I initially wanted to load the page the image can be viewed on within an `iframe`. As the requested page doesn't allow cross-origin framing, however, I opted for simply displaying the src image in full resolution.
- I'm using `lodash.debounce` for debouncing. The solution is being published under the `MIT` license.

### Potential improvements
- Design. The current design is very basic and far from pretty.
- Change all tag styling to class based styling. This might not be 100% necessary due to the `scoped` styling of `vueJS`.
- Grab information about the existence of the next page from the request header.
- Implement `srcSet` for images.
- Some of the functions within `App.vue` could be moved to their own `.js` files to improve readability.
- Instead of opening a lightbox on mobile, the image could either become fullscreen or open the url in a different tab.
- Implement filter for results by looking at the `images` object and searching through the `authors` contained within it.