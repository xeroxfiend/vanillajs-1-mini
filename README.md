<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250" align="right">

# Project Summary

In this project, we'll introduce you to vanilla JS DOM manipulation by creating a small project. The basic HTML and CSS have been provided for you, and you will be adding in the Javascript to make the interface interactive. The goal of this project is to create a simple counter interface that can use three different themes.

## Example

### Setup
Fork and clone this repository and open the folder in your code editor.

### Step 1

#### Summary

In this step, we'll create our Javascript file and connect it to our HTML.

#### Instructions

- Create a new file called `index.js`.
- Add a `console.log('hello world')` so we can see if the script is running.
- Open `index.html`
- Inside the `<body>` tag, but after the `<main>` element, add a `<script>` tag to bring in your `index.js` file.
- Open `index.html` in your web browser.
  - Open the console and look for the `hello world` console log from your Javascript file. If it doesn't appear, check the file path in your `<script>` tag.

#### Solution

<details>
<summary>
<code>/index.html</code>
</summary>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Theme Changing Counter</title>
    <link rel="stylesheet" href="./index.css" />
    <link rel="stylesheet" href="./themes.css" />
  </head>
  <body>
    <header>
      <p>Choose a theme:</p>

      <button>Facebook</button> <button>DevMountain</button>
      <button>Twitter</button> <button>Default</button>
    </header>
    <main>
      <h1>0</h1>
      <h2>Clicks</h2>
      <section>
        <button>-</button> <button>Reset</button> <button>+</button>
      </section>
    </main>
    <script src="./index.js"></script>
  </body>
</html>
```

</details>

### Step 2

#### Summary

In this step, we'll start working on the Javascript functions needed for the counter functionality in `index.js`

#### Instructions

- Create a global variable called `count` with an initial value of `0`. We will update this global variable in all of our functions.
- Next, create a function called `increase` that increases the value of `count` by 1. For now, `console.log` the new value of count so you can see when the function runs.
- Follow the same pattern to create a function called `decrease` that decreases the value of `count` by 1 and `reset` that resets the value of `count` to 0.

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
let count = 0;

function increase() {
  count++;
  console.log(count);
}

function decrease() {
  count--;
  console.log(count);
}

function reset() {
  count = 0;
  console.log(count);
}
```

</details>

### Step 3

#### Summary

In this step, we will update our HTML to run our Javascript functions when the buttons are clicked.

#### Instructions

- In `index.html`, find the `h1` element and add an `id` attribute with a value of `"counter"`.
  - We need an `id` for this element so we can update its text in Javascript in the next step.
- Find the `-`, `Reset`, and `+` buttons and add an `onclick` attribute.
  - The value of each `onclick` attribute should be one of the Javascript functions we created earlier invoked. Ex. `onclick="increase()"`
- With your console open, click the buttons to see if the function is running and the value of `count` is changing correctly.

#### Solution

<details>
<summary>
<code>/index.html</code></summary>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Theme Changing Counter</title>
    <link rel="stylesheet" href="./index.css" />
    <link rel="stylesheet" href="./themes.css" />
  </head>
  <body>
    <header>
      <p>Choose a theme:</p>

      <button>Facebook</button> <button>DevMountain</button>
      <button>Twitter</button> <button>Default</button>
    </header>
    <main>
      <h1 id="counter">0</h1>
      <h2>Clicks</h2>
      <section>
        <button onclick="decrease()">-</button>
        <button onclick="reset()">Reset</button>
        <button onclick="increase()">+</button>
      </section>
    </main>
    <script src="./index.js"></script>
  </body>
</html>
```

</details>

### Step 4

#### Summary

In this step, we will update our Javascript functions to update the content in the `h1` instead of displaying `count` in the console.

#### Instructions

- In `index.js`, use `document.getElementById` to create a new variable called `element` that references the `h1` element with an id of `counter` from `index.html`
- In your `increase` and `decrease` functions, use the `innerText` property of the `element` variable to change the value that is displayed in the `h1` with the new value of `count`.
- In your `reset` function, use the `innerHTML` property of the `element` variable to change its HTML to include a `<mark>` tag around the value of `count`.
- Remove your `console.log` in each function.

#### Solution

<details>
<summary>
<code>/index.js</code>
</summary>

```js
let count = 0;
const element = document.getElementById("counter");

function increase() {
  count++;
  element.innerText = count;
}

function decrease() {
  count--;
  element.innerText = count;
}

function reset() {
  count = 0;
  element.innerHTML = "<mark>" + count + "</mark>";
}
```

</details>

### Step 5

#### Summary

In this step, we will start working on the javascript functions needed to change the themes on the page. The themes are already provided for you in `themes.css` and do not need to be changed. Instead, we just need to add the correct class name to the `body`, `main` and `button` elements.

#### Instructions

- In `index.js`, create a function called `selectTheme` that takes in a string called `theme` as a parameter.
- Use `document.getElementsByTagName` to select the `body` element and change its `className` property to the `theme` variable.
  - Remember that `document.getElementsByTagName` returns a `NodeList`, which is similar to an array. You'll need to use square bracket notation to edit the `className` property of the first element in the `NodeList`
- Repeat this step for the `main` element.
- We will need to select all of the buttons in the `index.html` file. We can use `document.getElementsByTagName` to select all of them and assign them to a variable called `buttons`. We will to use a `for` loop to change the `className` property for every `button` element in the buttons variable. Remember, when selecting elements with `document.getElementsByTagName`, it returns a `NodeList` which is an array-like list.

#### Solution

<details><summary><code>/index.js</code></summary>

```js
function selectTheme(theme) {
  document.getElementsByTagName("body")[0].className = theme;
  document.getElementsByTagName("main")[0].className = theme;
  const buttons = document.getElementsByTagName("button");

  for (let i = 0; i < buttons.length; i++) {
    buttons[i].className = theme;
  }
}
```

</details>

### Step 6

#### Summary

In this final step, we will update our HTML to run the `selectTheme` function and pass in the appropriate parameter when a theme button is pressed.

#### Instructions

- In `index.html`, add an `onclick` attribute to each `button` inside the `header` element. The value for each attribute should be the invocation of the `selectTheme` function, passing in a string of the appropriate theme for each button -- `'facebook'`, `'devmountain'`, `'twitter'`, or `'default'`

#### Solution

<details><summary><code>/index.html</code></summary>

```html
<header>
  <p>Choose a theme:</p>

  <button onclick="selectTheme('facebook')">Facebook</button>
  <button onclick="selectTheme('devmountain')">DevMountain</button>
  <button onclick="selectTheme('twitter')">Twitter</button>
  <button onclick="selectTheme('default')">Default</button>
</header>
```

</details>

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2018. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250">
</p>
