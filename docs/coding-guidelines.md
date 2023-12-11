## Intro

These are our coding guidelines.

## Git

Please provide new code to our most recent development branch and not directly to the main branch.

## Indentation
We use 4 spaces, not tabs.

## Names
* Use camelCase for `function` and `method` names
* Use camelCase for `property` names and `local variables`
* Use whole words in names when possible

## Strings
* Use "double quotes" for strings

## Style
* Open curly braces always go on the same line as whatever necessitates them
* Parenthesized constructs should have no surrounding whitespace. A single space follows commas, colons, and semicolons in those constructs. For example:

```javascript
for (let i = 0, n = str.length; i < 10; i++) {
    if (x < 10) {
        foo();
    }
}

function f(x: number, y: string): void { }
```


Source: https://github.com/microsoft/vscode/wiki/Coding-Guidelines
