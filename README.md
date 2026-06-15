🎨 Creating a New Theme from Scratch
====================================

The default theme in the framework is **mizoon**,\
but you can easily create your own custom themes with different colors, fonts, and components.

### 🗂 1. Create Your Theme Folder

Inside the `themes/` directory, make a new folder for your theme, for example:

`themes/mizchin/ `

### ⚙️ 2. Copy the Config Folder

Take the whole `config` folder from the **mizoon** theme and paste it into your new theme:

`themes/mizchin/config/ `

Then open the files inside and adjust things like colors, fonts, or spacing to match your theme's style.


### 🎨 3. Important Note About Colors and Fonts

When you define new colors or fonts for your theme, make sure you **merge** them with the main framework's settings.\
That way, your theme will still stay compatible with the base system, while keeping its own look.

#### Example -- Colors:
```scss
// mizchin/config/_color.scss

$light-color-palette-theme: (
  primary: #ff6b6b,
  secondary: #ffe66d 
)
$light-color-palette: map.merge($light-color-palette, $light-color-palette-theme);
```
#### Example -- Fonts:
```scss
// mizchin/config/_font.scss

$fonts-theme: (
    "tektur": (
        "defaults":"'Brush Script MT',cursive",
        "folder": "Tektur",
        "font-types": (
            "bold": (
                "Tektur-Bold.ttf"
            ),
            "regular": (
                "Tektur-Regular.ttf"
            ),
        )
    ),
);
$fonts: map.merge($fonts, $fonts-theme);
```
💡 **Tip:** Merging makes sure your theme and the main system work together smoothly.

### ⚙️ 4. Enable or Disable the Theme

Open the `config.js` file and set your theme name to activate it:

```js 
export  const config = { theme: 'mizchin', output: "public/assets/js/mizchin.min.js" };
```

To **disable themes** completely (and just use the default framework settings):

### Config Behavior (Semantic Meaning)

```js
/**
 * config.theme semantic rules:
 *
 * - null → explicitly means the value is absent
 *   (disabled / not configured / ignored)
 *
 * - "" (empty string) → value exists but is intentionally empty
 *   (explicit override with no content)
 *
 * Note:
 * These are not just syntax differences — they represent different
 * semantic states of configuration.
 */
export const config = {
  theme: null, // absent (no theme configured)
  output: "public/assets/js/mizchin.min.js"
};
```

When `theme` is set to `null`, no theme is loaded --- only the base framework settings are used.



### 🧩 5. Create the Components Folder

Inside your theme folder, add a new folder called `components`:

`themes/mizchin/components/ `

In there, create a file named `_index.scss` --- this is where all your component styles will be connected.

Example:

`// mizchin/components/_index.scss  @forward  'button'; @forward  'card'; `

Each component you make should have its **own folder**, like this:

`button/
 ├── index.html ├── script.js └── _index.scss  `

-   `index.html`: the component's HTML structure

-   `_index.scss`: all related styles

-   `script.js`: JavaScript behavior for that component

* * * * *

### 🎯 6. Connect Components to the Theme

In your theme's main `_index.scss`, forward both the `config` and `components` folders:

`// mizchin/_index.scss  @forward  'config/_index'; @forward  'components/_index'; `

This links all your configuration and component files to your theme.

* * * * *

### ✅ Final Structure

Here's what your theme folder should look like when everything's ready:

`themes/
 ├── mizoon/
 └── mizchin/
     ├── _index.scss
     ├── config/
     │    ├── _color.scss
     │    ├── _font.scss
     │    └── ...
     └── components/
          ├── _index.scss
          ├── button/
          │    ├── index.html
          │    ├── _index.scss
          │    └── script.js
          └── card/
               ├── index.html
               ├── _index.scss
               └── script.js`
