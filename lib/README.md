# react-tinted

Tinted is a color harmony wheel. It helps you choose color combinations that create pleasing contrasts and feel harmonious.

[Demo](https://zposten.github.io/tinted)

## Install

```bash
# Install with yarn
yarn add react-tinted

# Or install with NPM
npm i react-tinted
```

## Usage

```jsx
import {TintedWheel, TintedPalette, colorModes} from 'react-tinted'
```

```jsx
<div className='my-color-wheel'>
  <TintedWheel colorCount={5} mode={colorModes.ANALOGOUS}>
    <TintedPalette />
  </TintedWheel>
</div>
```

```scss
@use 'tinted/wheel';
@use 'tinted/palette';

.my-color-wheel {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: auto;
  max-width: 400px;
}
```

A few things to note:

- The wheel can be used without the palette, but it is recommended to use them together.
- To make these abbreviated `@use` statements work, you will need to add `node_modules` to SASS' `--load-path` or sass-loader's `includePaths`. Alternatively, you could just path into `node_modules` explicitly.
- If you're not using SASS in your project, we do provide compiled CSS files in the `tinted/dist` folder.

## Custom Colors

You can initialize Tinted with a custom color set:

```jsx
<TintedWheel
  mode={colorModes.CUSTOM}
  customColors={[
    'red',
    '#0ff',
    {r: 0, g: 255, b: 0},
    {h: 220, s: 1, v: 1},
    {h: 300, s: 1, l: 0.5},
    'hsl(0, 100%, 50%)',
  ]}
>
  <TintedPalette />
</TintedWheel>
```

## Components

### TintedWheel

The color harmony wheel for the user to make a selection of colors.

#### Props

| Name                 | Type                                            | Description                                                                                                                                                       |
| -------------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `children`           | `React.Children`                                | Color wheel "plugins" like the `TintedPalette`                                                                                                                    |
| `className`          | `string`                                        | A class name to add to the root element                                                                                                                           |
| `colorCount`         | `number`                                        | The number of colors to use in the color harmony                                                                                                                  |
| `initRoot`           | color-like value                                | The color that should initially be used to select other harmony colors                                                                                            |
| `customColors`       | color-like array                                | Rather than specify a root color and a color count, you can pass an array of color-like objects and strings                                                       |
| `mode`               | `string`                                        | The color harmony mode. Determines how `initRoot` is used to find other colors                                                                                    |
| `colorWheelImage`    | `string`                                        | A URI to a color HSV color wheel image to use                                                                                                                     |
| `onColorsChanged`    | `(hexColorStrings, currentMode, wheel) => void` | Callback invoked when the user manipulates the color markers                                                                                                      |
| `radius`             | `number`                                        | The radius of the wheel in SVG coordinate units                                                                                                                   |
| `markerWidth`        | `number`                                        | The diameter of the markers used to select colors on the wheel in SVG coordinate units                                                                            |
| `markerOutlineWidth` | `number`                                        | The width of the outline of the color marker in SVG coordinate units                                                                                              |
| `margin`             | `number`                                        | The distance between the border of the `<svg>` and the circle of the wheel in SVG coordinate units. It is not recommended to pass this prop                       |
| `baseClassName`      | `string`                                        | The prefix for the class names for all generated elements. Overriding this will cause all provided CSS to no longer work. It is not recommended to pass this prop |

Also spreads any other props passed on the root element.

### TintedPalette

A palette of colors to display the user's chosen values from the `TintedWheel`. For each color it:

- Allows the user to change the value (or brightness -- "V" in the HSV color model) of the color
- Displays the hex string value of the color

#### Props

| Name        | Description                                                   |
| ----------- | ------------------------------------------------------------- |
| `children`  | An element to be duplicated beneath each color in the palette |
| `className` | A class name to add to the root element                       |

Also spreads any other props passed on the root element.

## Styling

Feel free to override any of the default styling as you please.

Out of the box, tinted supports a color scheme for a light and dark background, defaulting to the light background. To change it to expect a dark background, add a `tinted--dark` class to a parent element of the wheel and/or palette.
