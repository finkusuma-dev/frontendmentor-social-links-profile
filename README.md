# Notes

## Links

Live URL: https://finkusuma-dev.github.io/frontendmentor-social-links-profile/.

## CSS Implementation

- Defined properties that are using px/rem unit to determine which properties that need to be scaled along with the default font size.
  - `max-width`: rem.
  - `padding`: px.
  - `gap`: rem.
  - width & height of `img`: px.
- Remove `px` from spacing variables, so I can use it with px/rem unit.
- Setup text preset variables to use in the CSS `font` property.

  `700 calc(24rem / 16) / 1.5 'Inter', sans-serif;` = `[font weight] [font size] / [line-height] [font-family]`

## CSS Issues

- FIXME: The card's width is narrower than 327px. Probably a problem using flex to center container. `flex-direction` is set to `column`, but it shrinks the cross axis.

  The problem doesn't have to do with flex. But the most wide element inside the card is the description, which occupies less than 327px-(2x24px). If added 3 or more characters, the max-width is fulfilled (327px).
