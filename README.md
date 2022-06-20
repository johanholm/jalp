# Jalp

Jalp is a set of sass helpers that helps create beautifully responsive websites.

**Jalp is currently in development and new features will be implemented soon.**

## Quick start

Install with yarn: `yarn add jalp`

---

## Fluid size Interpolation

Fluid responsive attribute sizing

### Usage

```scss
@use "jalp";

h1 {
  // Any attribute, like font-size, width, height etc can be used
  @include jalp.fluid(font-size, 14px, 12px, 16px, 18px);

  // Alternatively a map of attributes can be sent in like so
  @include jalp.fluid((width, height), 14px, 12px, 16px, 18px);
}
```

### Result

```scss
h1 {
  // This is the "mobile" version and will fall back under the 767px screen size
  font-size: 14px;
}
@media screen and (min-width: 767px) {
  h1 {
    // Is equal to 12px on 767px screen width
    // and will go from 12px to 16px before the next breakpoint will kick in
    font-size: calc(0.6677vw + 6.8781px);
  }
}

@media screen and (min-width: 1366px) {
  h1 {
    // Is equal to 16px on 1366px screen width
    // and will go from 16px to 18px before the next breakpoint will kick in
    font-size: calc(0.361vw + 11.0685px);
  }
}
@media screen and (min-width: 1920px) {
  h1 {
    // Is equal to 18px on 1920px screen width, and will scale up from there
    font-size: 0.9375vw;
  }
}
```

### The diffirent breakpoints can be overwritten

```scss
@use "jalp" with (
  $breakpoints: (
    tablet: 767px,
    desktop-min: 1366px,
    desktop: 1920px,
  )
);
```

### Alternatively you can create your own file and set the default variables in there, and then use that file instead of 'jalp'

```scss
// functions.scss
@forward "jalp" with (
  $breakpoints: (
    tablet: 767px,
    desktop-min: 1366px,
    desktop: 1920px,
  )
);

// heading.scss
@use "./functions";

h1 {
  @include functions.fluid(font-size, 14px, 12px, 16px, 18px);
}
```
