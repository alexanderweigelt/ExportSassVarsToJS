# Exporting SCSS Variables to JavaScript with Webpack 5

In contemporary web development, maintaining a clear separation of concerns is a paramount practice. While Cascading
Style Sheets (CSS) handle styling, JavaScript (JS) takes charge of interactivity. However, there are instances where
bridging the gap between these two realms becomes essential, particularly when dealing with dynamic styles. I
will walk you through the process of exporting SCSS variables to JavaScript using Webpack 5, a prominent JavaScript
module bundler. Additionally, I'll explore how to enable interoperable CSS functions like `:import` and `:export`
directly in the `css-loader` using the `mode: "icss"` option, and provide a comprehensive example of configuring
your `webpack.config.js` file.

## Why Export SCSS Variables to JavaScript?

1. **Dynamic Theming:** Exporting SCSS variables to JavaScript empowers dynamic theming. This means you can seamlessly
   alter the website's color scheme, typography, or other visual aspects on-the-fly, based on user preferences,
   interactions, or other dynamic conditions.

2. **Conditional Styling:** It enables conditional styling, such as implementing a dark mode feature. By manipulating
   SCSS variables in JavaScript, you can adjust styles in response to user choices and actions.

3. **Reusable Styles:** SCSS variables can store reusable styles, such as font sizes, spacing values, or breakpoints. By
   exporting them to JavaScript, you can employ these values consistently across different components or modules.

## Enabling Interoperable CSS Functions with `css-loader`

To facilitate the export of SCSS variables to JavaScript, we can enable interoperable CSS functions directly within
the `css-loader`. Webpack 5's `css-loader` supports this functionality through the `mode: "icss"` option. Here's how to
configure your `webpack.config.js` to allow interoperable CSS functions using this approach:

```javascript
const path = require('path');

module.exports = {
    // ...other webpack config options
    module: {
        rules: [
            // ...other rules
            {
                test: /\.scss$/,
                use: [
                    'style-loader',
                    {
                        loader: 'css-loader',
                        options: {
                            importLoaders: 1,
                            modules: {
                                mode: "icss", // Enable ICSS (Interoperable CSS)
                            },
                        },
                    },
                    'sass-loader',
                ],
            },
        ],
    },
};
```

In this configuration:

- We specify the `mode: "icss"` option within the `css-loader` configuration to enable Interoperable CSS (ICSS),
  allowing the use of `:export` and `:import` within SCSS files.

## Exporting SCSS Variables

With the `mode: "icss"` option enabled in the `css-loader`, you can effortlessly export SCSS variables in your SCSS
files:

```scss
// variables.scss
$primary-color: #3498db;
$secondary-color: #e74c3c;

:export {
  primaryColor: $primary-color;
  secondaryColor: $secondary-color;
}
```

In this example, we define two SCSS variables (`$primary-color` and `$secondary-color`) and utilize the `:export`
function to make them available for JavaScript consumption as `primaryColor` and `secondaryColor`.

## Accessing SCSS Variables in JavaScript

Now that your SCSS variables are set up for export, you can access them within your JavaScript code:

```javascript
// app.js
import styleVars from './variables.scss';

console.log(styleVars.primaryColor); // #3498db
console.log(styleVars.secondaryColor); // #e74c3c
```

In this example, we import the SCSS file where the variables are exported and access them as properties of
the `styleVars` object.

## Conclusion

Exporting SCSS variables to JavaScript via Webpack 5's `css-loader` with the `mode: "icss"` option is a robust technique
that facilitates dynamic, user-centric web applications. By enabling interoperable CSS functions, you can seamlessly
integrate your styling and JavaScript logic. This approach enhances code maintainability, encourages reusability, and
empowers you to create captivating and responsive user experiences.

## Development

First install dependencies:

```
npm install
```

To create a production build:

```
npm run build
```

(bundles your application)
