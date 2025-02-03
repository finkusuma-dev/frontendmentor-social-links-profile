# Frontend Mentor - Social links profile solution

This is a solution to the [Social links profile challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/social-links-profile-UG32l9m6dQ). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Frontend Mentor - Social links profile solution](#frontend-mentor---social-links-profile-solution)
  - [Table of contents](#table-of-contents)
  - [Overview](#overview)
    - [The challenge](#the-challenge)
    - [Screenshot](#screenshot)
    - [Links](#links)
  - [My process](#my-process)
    - [Built with](#built-with)
    - [What I learned](#what-i-learned)
      - [🟦 No Longer Use "Font Size Hack"](#-no-longer-use-font-size-hack)
      - [🟦 Use Both `px` and `rem` Units](#-use-both-px-and-rem-units)
      - [🟦 Removed `px` from CSS Spacing Variables](#-removed-px-from-css-spacing-variables)
      - [🟦 Setup CSS Text Preset Variables](#-setup-css-text-preset-variables)
      - [🟦 `:focus-visible` Class Selectors](#-focus-visible-class-selectors)
      - [🟦 Solved: Card's Width Shrinks when Using `max-width`](#-solved-cards-width-shrinks-when-using-max-width)
        - [**Before and after the fix**](#before-and-after-the-fix)
      - [🟦 Removed `<nav>` Wrapping The Links](#-removed-nav-wrapping-the-links)
    - [Continued development](#continued-development)
    - [Useful resources](#useful-resources)
  - [Author](#author)

## Overview

### The challenge

Users should be able to:

- See hover and focus states for all interactive elements on the page

### Screenshot

<img src="./_docs/screenshot.jpg" width="300"/>

### Links

- Solution URL: [Add solution URL here](https://your-solution-url.com)
- Live Site URL: [https://www.frontendmentor.io/challenges/social-links-profile-UG32l9m6dQ](https://www.frontendmentor.io/challenges/social-links-profile-UG32l9m6dQ)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- Mobile-first workflow

### What I learned

#### 🟦 No Longer Use "Font Size Hack"

"Font Size Hack" is a trick to setting the font size to make it easier to write rem unit. I first knew about it from some Udemy course and I've been using it since. After read about blogs of senior web devs [^1][^2], I'm convinsed that it's better not to use it. For me the most convinsing reason is that, it will screw up the project when you insert any code that is made without the "Font Size Hack", into your code that use the "Hack", or vice versa.

What I found is actually you can use it, if you only build your own project that doesn't need any 3rd party code. But when you start to incorporate someone else code, or you start collaborating, or even further when you start working on a company, it's strongly adviced not to use it. As the most web developers out there never use it too.

So, in this challenge I use CSS `calc()` to set the values in rem.

```css
hgroup {
  gap: calc(var(--spacing-50) / 16 * 1rem);
}
```

#### 🟦 Use Both `px` and `rem` Units

Before, I always used rem in all of the CSS size properties. After reading explanation on Josh's blog [^2], it just makes sense to use both `px` and `rem`. We just need to know what are the properties that need `px` or `rem`, and why. Josh explains it very clearly in his blog, and no need to memorize it. When working on this challenge I didn't lookup what the props are. After coding px/rem was completed, I checked it and everything was correct. Josh teaching style is really awesome and I recommend you to read about other things too in [his blog](https://www.joshwcomeau.com).

Below is the list of properties that use px/rem unit. In summary, if you need a prop to be scaled along with the default font size, use `rem`. Otherwise, use `px`.

- `font-size`: rem.
- `max-width`: rem.
- `padding`: px.
- `gap`: rem.
- width & height of `img`: px.
- `border-radius`: px.

#### 🟦 Removed `px` from CSS Spacing Variables

The Figma spacing design tokens have `px` unit attached. So I removed the unit and set it later using `calc()` function.

```css
:root {
  --spacing-300: 24;
}

.card {
  /* use px unit */
  padding: calc(var(--spacing-300) * 1px);

  /* use rem unit */
  gap: calc(var(--spacing-300) / 16 * 1rem);
}
```

#### 🟦 Setup CSS Text Preset Variables

In the figma file, there are text preset design tokens containing font family, font weight, font size, line height, and letter spacing on each of the preset. I setup variables to hold these values, and then use it later by assigning it to the font property.

```css
:root {
  --text-preset-1: 700 calc(24rem / 16) / 1.5 'Inter', sans-serif;
  /* ([font weight] [font size] / [line-height] [font-family]) */
}

h1 {
  font: var(--text-preset-1);
}
```

#### 🟦 `:focus-visible` Class Selectors

There are two class selectors for element that currently in focus: `:focus` and `:focus-visible`. (Actually three, but this solution only implements two.)

From my testing, the difference between the two:

- When using `:focus` on an anchor link, and the link is clicked/tapped it will show the focus ring.
- While using `:focus-visible`, when the link is clicked/tapped it won't show the focus ring.

While using keyboard `tab` key to change focus, both showing the focus ring.

On this solution, I use `:focus-visible` on the anchor links:

```css
ul.links {
  a:focus-visible {
    outline: 1px solid var(--color-green);
  }
}
```

and `:focus` on the attribution links:

```css
.attribution {
  a:focus {
    outline: 1px solid var(--color-white);
    border-radius: 1px;
  }
}
```

#### 🟦 Solved: Card's Width Shrinks when Using `max-width`

I set the card's `max-width` to `327px` (mobile first). Then centering the card using flexbox and set the `flex-direction` to column. The problem arises when I set up the `align-items` to `center`. The cross axis (horizontal axis) shrinks to less than `327px`.

The issue is caused by the most wide child element in the card: the description:

```html
<p>Front-end developer and avid reader.</p>
```

The total length of the `p` element is `255.9px`, added two paddings of `24px`, hence the card's width shrinks to `303.9px`.

In my testing, this happens also when the card is put inside a container and the container `width` is set to `fit-content`.

After trials, I concluded there are two ways to solve this:

1. Keep using `max-width`, but using another method to center the card.

   I know this method from a Udemy course, apparantly it's able to solve this problem. The method is using `margin-inline: auto` to make the card center horizontally and `top: 50%; transform: translateY(-50%)` to center vertically.

   ```css
   .card {
     margin-inline: auto;
     top: 50%;
     transform: translateY(-50%);
   }
   ```

   `top: 50%` means, the top position is calculated by using 50% of the card' parent element. And `-50%` on the transform property means, the card is translated in the negative Y axis (up direction) by 50% of the card's height.

2. Using `width` instead of `max-width`.

   Using `width` and by utilizing `min()` function, to choose between minimum values of 327px and 100% viewport width. If width of the viewport is more than 327px, card's width will be constrained to 327px. If less, car's width will be calculated using 100% viewport width minus paddings.

   And also to set the card's minimum width to `min-content`. Although there is no screen size that really that small, I think this is a good practice.

   ```css
   .card {
     width: min(calc(327rem / 16), calc(100vw - (20px)));
     min-width: min-content;
   }
   ```

   | With `min-content`                                | Without `min-content`                                |
   | ------------------------------------------------- | ---------------------------------------------------- |
   | <img src="./_docs/min_content.jpg" height="300"/> | <img src="./_docs/no_min_content.jpg" height="300"/> |

##### **Before and after the fix**

Before:

<img src="./_docs/width_shrink.jpg" width="300"/>

After:

<img src="./_docs/width_shrink_fix.jpg" width="300"/>

#### 🟦 Removed `<nav>` Wrapping The Links

Reading the Webdev navigation [^3], I was unsure whether or not I should use `nav` element to wrap the links. The document mentions 5 type of navigations, and all are related with the pages within the website. It doesn't mention of a page consisting only links to other websites.

Thanks to discord member @Darkstar, who confirmed to not use the `nav`.

### Continued development

Use this section to outline areas that you want to continue focusing on in future projects. These could be concepts you're still not completely comfortable with or techniques you found useful that you want to refine and perfect.

### Useful resources

- https://developer.mozilla.org/en-US/docs/Web/CSS/font, MDN doc CSS `font` property.
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hgroup, MDN doc `hgroup`.
- https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible, MDN doc `:focus-visible`.

(Note: Other resources are listed as footnote on the bottom of this README.)

## Author

- Github - [https://github.com/finkusuma-dev](https://github.com/finkusuma-dev)
- Frontend Mentor - [@finkusuma-dev](https://www.frontendmentor.io/profile/finkusuma-dev)
- Twitter - [@finkusuma_dev](https://www.twitter.com/finkusuma_dev)

[^1]: https://fedmentor.dev/posts/rem-html-font-size-hack/ Grace Snow's blog about font size hack.
[^2]: https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/ Josh W Comeau's blog about how to choose which properties to use px/rem unit. Also mentions to not use the "font size hack" at the end as well.
[^3]: https://web.dev/learn/html/navigation, Webdev navigation guide.
