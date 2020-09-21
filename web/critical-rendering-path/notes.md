# CRP Notes

[https://developers.google.com/web/fundamentals/performance/critical-rendering-path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path)

## Constructing the Object Model

- Bytes → characters → tokens → nodes → object model.
- HTML markup is transformed into a Document Object Model (DOM); CSS markup is transformed into a CSS Object Model (CSSOM).
- DOM and CSSOM are independent data structures.
- Chrome DevTools Timeline allows us to capture and inspect the construction and processing costs of DOM and CSSOM.

## Render-tree Construction, Layout, and Paint

- The DOM and CSSOM trees are combined to form the render tree.
- Render tree contains only the nodes required to render the page.
- Layout computes the exact position and size of each object.
- The last step is paint, which takes in the final render tree and renders the pixels to the screen.

## Render Blocking CSS

- By default, CSS is treated as a render blocking resource.
- **Media types and media queries allow us to mark some CSS resources as non-render blocking.**
- The browser downloads all CSS resources, regardless of blocking or non-blocking behavior.

## Adding Interactivity with Javascript

- JavaScript can query and modify the DOM and the CSSOM.
- **JavaScript execution blocks on the CSSOM.**
- **JavaScript blocks DOM construction unless explicitly declared as async.**

- The location of the script in the document is significant.
- **When the browser encounters a script tag, DOM construction pauses until the script finishes executing.**
- JavaScript can query and modify the DOM and the CSSOM.
- **JavaScript execution pauses until the CSSOM is ready.**

> To a large degree, "optimizing the critical rendering path" refers to understanding and optimizing the dependency graph between HTML, CSS, and JavaScript.
