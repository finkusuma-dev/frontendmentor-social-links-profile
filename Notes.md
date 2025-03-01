# Notes

## Links

- Live URL: https://finkusuma-dev.github.io/frontendmentor-social-links-profile/
- Challenge URL: https://www.frontendmentor.io/challenges/social-links-profile-UG32l9m6dQ

## CSS Implementation

- Defined properties to use px/rem unit to determine which need to be scaled along with the default font size. [^1]
  - `font-size`: rem.
  - `max-width`: rem.
  - `padding`: px.
  - `gap`: rem.
  - width & height of `img`: px.
  - `border-radius`: px.
- Removed `px` from spacing variables, so it can be use with px/rem unit.
- Setup text preset variables to use in the CSS `font` property. [^2]

  ```css
  --text-preset-1: 700 calc(24rem / 16) / 1.5 'Inter', sans-serif;
  /* ([font weight] [font size] / [line-height] [font-family]) */

  font: var(--text-preset-1);
  ```

- Using `:focus-visible` class selector instead of `:focus` on the anchor link, so when clicked/tapped it won't show the focus ring.

  When using `:focus` class selector, click/tap will show the focus ring, like you see on the attribution.

## CSS Issues

### (Solved): The Card's Width Narrower Than 327px.

When using flex to center container. Setting `align-items: center` makes the cross axis shrinks to less than the `max-width`.

The most wide element inside the card is the description, which occupies less than 327px-(2x24px padding). Setting the flex `align-items` to `center` shrinks the width of children elements to `fit-content` width. This behaviour is the same when the card is wrapped with a container and the container's `width` is set to `fit-content`.

There are two ways to solve this:

1. Keep using `max-width`, but applying another method to center the card. Set
   `margin-inline: auto` to make the card center horizontally and `top: 50%; transform: translateY(-50%)` to center vertically.

   ```css
   .card {
     margin-inline: auto;
     top: 50%;
     transform: translateY(-50%);
   }
   ```

2. Using `width` instead of `max-width`.

   Set the card's width by utilizing `min()` function, to choose between minimum values of 327px and 100% viewport width. If the width of viewport is more than 327px it will be constrained to 327px. If less it will be calculated using 100% viewport width minus padding.

   And the last thing is to set the card's minimum width to `min-content`. Although there is no screen size that really that small, I think it's a good practice.

   ```css
   .card {
     min-width: min-content;
     width: min(calc(327rem / 16), calc(100vw - (20px)));
   }
   ```

   | With `min-content`                                | Without `min-content`                                |
   | ------------------------------------------------- | ---------------------------------------------------- |
   | <img src="./_docs/min_content.jpg" height="300"/> | <img src="./_docs/no_min_content.jpg" height="300"/> |

## TODOs

- [x] Find more about `:focus-visible` class selector.
- [x] Read more about nested CSS feature.

[^1]: https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/.
[^2]: https://developer.mozilla.org/en-US/docs/Web/CSS/font.
