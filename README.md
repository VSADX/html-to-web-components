# Write WebComponents from regular HTML
```html
<div>
  <h1>
    If only we didn't
    <small>           
                      need to write JS to create small custom elements 
    </small>
  </h1>
  <style>
    small { display: block; font-size: .4em; }
  </style>
</div>
```
Wait, why browser WebComponents anyway?
+ Convert entire footers or navbars to one line of readable HTML
+ CSS is easier to write inside WebComponents, no JS needed for magic here
+ WebComponents add more features to typical HTML so you write less JS
+ Your sites go faster since a component is only parsed once no matter how much you use it!
```html
<xmp component-name="nav-bar">

  <h1> 
        What is the xmp element? 
    
        What does component-name do? 
  </h1>
  
</xmp>
```
**Here's a little trick.**  
  
We're using the old `<xmp>` element. Totally deprecated, but VSCode (most IDEs) 
think it is like any `<div>`. They're wrong. Anything you put inside this element 
the browser will see as raw text. That means we can parse it XML-style.  
  
**You want me to write XML?**  
  
Yep, this literally adds features to HTML like case-sensitive element attributes. It 
adds the ability to close any element `<img />`-style. So your custom elements can 
take advantage of this no problem:
```html
<my-custom-component />
```
Of course, nothing stops you from doing it the old way:
```html
<my-custom-component></my-custom-component>
```
  
**So what does `component-name="some-name"` do?**  
  
That's how you name your custom element! Those `<xmp>` tags won't show up when your component loads, 
the `<xmp>` tag name is replaced by the name you chose. Here's an example (that's what xmp stands for).  
  
```html
<xmp component-name="blog-footer">
 ...
</xmp>
```
When the page loads, inspect element, here's what you'll see when you use your element.
```html
<blog-footer>
 ...
</blog-footer>
```
  
<br>  
  
> Browsers have been supporting WebComponents for awhile now, let's make them easier to use by 
letting you create them from HTML/CSS.  
  
<br>
  
## Really powerful features for HTML
```html
<xmp component-name="my-price-ticker">

  <p> Signed in as: ${this.name} </p>
  
  <a prop:href=${ this.logout_url } prop:hidden=${this.is_logged_in}>
    Logout? 
  </a>
  
  <a prop:href=${ this.signup_url } prop:hidden=${!this.is_logged_in}> 
    Sign up! 
  </a>
  
</xmp>
```
  
**You can pass around JavaScript objects or functions directly in HTML**
If you've used JSX you've done this, but this is HTML - how does it work? 
Don't worry, we aren't bundling a parser, but you can use JavaScript variables 
directly in your HTML. You can even include a small script in your component 
to add or modify variables.
  
Here's an example of a full component:  
```html
<xmp data-component="nav-bar">

  <a href="/home"> Home </a>
  <a href="/about"> About </a>
  <a href="/contact"> Contact us! </a>
  
  <style>
    a:nth-child(${this.currentPageIndex}) /* <---- wait, JS variables in CSS */
    {
      color: red;
    }
  </style>
</xmp>
```
Here's how you use it:
```html
<nav-bar prop:currentPageIndex=${2} />

<!-- we're using case-sensitive attributes + self-closing tags, XHTML had this first -->
```
  
<br><br>  
  
### JavaScript + HTML
`simple-math.html`
```html
<div data-component="simple-math">
  <input prop:value=${first_num} />
  <input prop:value=${second_num} />
  <h2>Answer: ${result}</h2>
  
  <script type="module">
    const first_num = reactive(5)
    const second_num = reactive(10)

    computed(() => first_num.value + second_num.value)
  </script>
</div>
```    
  
## Notes / References
### JS in HTML support for VSCode
+ vscode has only some JavaScript autocomplete.
+ The vscode extension `shuaihu.html-embedded-javascript` has better support.
+ ext HEJ keeps emmet / html autocomplete
+ if you install it, you will want to disable emmet / html
1. In extesion search, paste: `@builtin html language features`
2. Disable ext
3. In extension search, paste: `@builtin emmet`
4. Disable ext
