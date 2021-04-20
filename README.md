# HTML to Web Components
## Example
### HTML Only Web Components
`my-component.html`
```html
<div data-component="my-thing">
  <h1>
    Hi!
    <small> We can convert this into a Web Component </small>
  </h1>
  <style>
    h1 { color: firebrick; }
    small {
      display: block;
      font-size: .6em;
      color: #0009;
    }  
  </style>
</div>
```
You can use it like this:
```html
<my-thing></my-thing>
```
### JavaScript + HTML
`simple-math.html`
```html
<div data-component="simple-math">
  <input bind:value=${first_num} />
  <input bind:value=${second_num} />
  <h2>Answer: ${result}</h2>
  
  <script type="module">
    const first_num = reactive(5)
    const second_num = reactive(10)

    computed(() => first_num.value + second_num.value)
  </script>
</div>
```
  
## Notes
### JS in HTML support for VSCode
+ vscode has only some JavaScript autocomplete.
+ The vscode extension `shuaihu.html-embedded-javascript` has better support.
+ ext HEJ keeps emmet / html autocomplete
+ if you install it, you will want to disable emmet / html
1. In extesion search, paste: `@builtin html language features`
2. Disable ext
3. In extension search, paste: `@builtin emmet`
4. Disable ext
