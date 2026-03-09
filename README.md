# HTML Template Repository with HTML Proofer

This template repository includes preconfigured GitHub Action that will validate html files in a project with (HTMLProofer)[https://github.com/gjtorikian/html-proofer/].
And htmx to load partials

```html
<main data-hx-trigger="load" data-hx-swap="outerHTML" data-hx-get="index.main.partial.html"></main>
```


```js
function init() {
    import('...js');
}

const totalPartials = document.querySelectorAll('[hx-trigger="load"], [data-hx-trigger="load"]').length;
let loadedPartialsCount = 0;

document.body.addEventListener('htmx:afterOnLoad', () => {
    loadedPartialsCount++;
    if (loadedPartialsCount === totalPartials) init();
});
```

Add the data-proofer-ignore attribute to any tag to ignore it from every check.

```html
<a href="https://notareallink" data-proofer-ignore>Not checked.</a>
```

## Synthetic review PRs

This repository also creates a synthetic pull request for every push to `main`.

- `review-base/...` points to the branch tip before the push
- `review-head/...` points to the branch tip after the push
- the synthetic PR diff shows the full `before..after` bundle, including multi-commit pushes and merge commits

That gives students PR-style review UI after direct pushes, while the existing `HTML Proofer` workflow still runs as a normal PR check on the generated review PR.

To let the workflow open pull requests, enable `Settings -> Actions -> General -> Workflow permissions -> Allow GitHub Actions to create and approve pull requests`.
