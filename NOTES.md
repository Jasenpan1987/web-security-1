# 1. XSS

## 1.1 Types of xss (danger zone)

- **stored xss:** code that executes attacker's script is persisted

- **reflected xss:** transient response from server causes script to execute (i.e. validation errors)

- **dom based xss:** no server involvement is required (i.e. pass code via queryParams)

- **blind xss:** exploit vulnerability in another app (i.e. log-reader), that the attackers can't see or access under the normal means

## 1.2 Place of xss

- under generated rich text (i.e. WYSIWYG)
- enbedded content
- anywhere the users have control over a url
- anywhere the users have input that relected back (i.e. "could not found xxx")
- query parameter rendered into a dom
- element.innerHTML = xxx

## In test project

user1:
test@test.com
Abcd1234

## 1.3.1 Attack #1

1. find an input box, try to add some html tags, such as `<b>hello</b>`, if it parses the html, that means there is a vulnerablity, we more likely to be able to add some `<script>` tags...

2. check the address bar, if it has some routes like `http:localhost:3000/jasenpan`, and on the web page, it says something like "welcome jasenpan!", try add `<script>console.log("hi")</script>` there, if we can see the output, it means there is a vulnerability, we can add `<script>` tags too...

## 1.3.2 Defend

### NEVER trust user data

- Directly in a script tag: `<script><%- userData -%></script>`
- In an html comment: `<!-- <%- userData -%> -->`
- In an attribute name: `<iframe <%- userData -%>="my-value" />`
- In a tag name: `<<%- userData -%> class="my-class" />`
- Directly in a style block: `<style><%- userData -%></style>`

### After run your code on the modern browsers, try them on old browsers too, although the frameworks / libraries says they not support IE7. Older browsers always more vulnerable than the modern ones.

### Sanitizing User data

In template engines (ejs), there are options that can sanitizing the user data. Never use the `escape` data. In react, don't use `dangerslySetInnerHTML`. And also be very carefully when templating the JS

```html
<script>
getUserData(<%- userId %>)
</script>
```

Always treat user input values as values, never treat them as code.
