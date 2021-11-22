<!-- markdownlint-disable MD033 MD036 MD041 -->

# use-tailwind-breakpoint

![npm](https://badgen.net/npm/v/@kodingdotninja/use-tailwind-breakpoint)
![packagephobia/install](https://badgen.net/packagephobia/install/@kodingdotninja/use-tailwind-breakpoint)
![packagephobia/publish](https://badgen.net/packagephobia/publish/@kodingdotninja/use-tailwind-breakpoint)

Custom hooks to use Tailwind CSS breakpoints for React 🎐🔨

---

**Table of contents**

- [Installing](#installing)
- [Usage](#usage)
  - [Option #1: Resolve directly from `tailwind.config.js`](#option-1-resolve-directly-from-tailwindconfigjs)
  - [Option #2: Only pass breakpoint values](#option-2-only-pass-breakpoint-values)
- [Available hooks](#available-hooks)
  - [`useBreakpoint()`](#usebreakpoint)
  - [`useBreakpointEffect()`](#usebreakpointeffect)
  - [`useBreakpointValue()`](#usebreakpointvalue)
- [Suggestions and/or questions](#suggestions-andor-questions)
- [Maintainers](#maintainers)
- [License](#license)

---

## Installing

```sh
# using npm
npm install @kodingdotninja/use-tailwind-breakpoint

# using yarn
yarn add @kodingdotninja/use-tailwind-breakpoint
```

## Usage

### Option #1: Resolve directly from `tailwind.config.js`

[Similar to `pmndrs/zustand`'s `create` API](https://github.com/pmndrs/zustand/#first-create-a-store), initialize the breakpoint hooks by passing the `tailwind.config.js` which will be resolved internally using [`resolveConfig`](https://github.com/tailwindlabs/tailwindcss/blob/master/src/util/resolveConfig.js):

```ts
// /hooks/tailwind.ts

import create from "@kodingdotninja/use-tailwind-breakpoint";

import tailwindConfig from "path/to/tailwind.config.js";

export const { useBreakpoint } = create(tailwindConfig);
```

> ⚠️ This possibly imports all `tailwind.config.js` values. Make sure to check the client bundle size.

### Option #2: Only pass breakpoint values

Extract the [`screens`](https://tailwindcss.com/docs/breakpoints) values into a separate file:

```js
// tailwind.screens.js or other name to separate breakpoint values
const screens = {
  sm: "640px",
  md: "768px",
  // ...
};
```

To keep the same values, `require` inside `tailwind.config.js`:

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      screens: require("path/to/tailwind.screens.js"),
    },
  },
  // ...
};
```

Then pass the extracted `screens` to the `create` function:

```ts
// /hooks/tailwind.ts

import create from "@kodingdotninja/use-tailwind-breakpoint";

import tailwindScreens from "path/to/tailwind.screens.js";

export const { useBreakpoint } = create(screens);
```

## Available hooks

### `useBreakpoint()`

Use breakpoint value from given breakpoint token

```jsx
import { useBreakpoint } from "./lib/";

function App() {
  const isDesktop = useBreakpoint("md");

  return <div>Current view: {isDesktop ? "Desktop" : "Mobile"}</div>;
}
```

### `useBreakpointEffect()`

Use given breakpoint value to run an effect

```jsx
import { useBreakpointEffect } from "@kodingdotninja/use-tailwind-breakpoint";

function App() {
  useBreakpointEffect("md", (match) => {
    if (match) {
      console.log("Desktop view");
    }
  });
}
```

### `useBreakpointValue()`

Resolve value from given breakpoint value

```jsx
import { useBreakpointValue } from "@kodingdotninja/use-tailwind-breakpoint";

function App() {
  const value = useBreakpointValue("md", "Desktop", "Mobile");

  return <div>Current view: {value}</div>;
}
```

## Suggestions and/or questions

Head over to our [dedicated Discord channel for `use-tailwind-breakpoint`](https://discord.gg/Zrfr7VqtpR).

## Maintainers

- Griko Nibras ([@grikomsn](https://github.com/grikomsn))

## License

[MIT License, Copyright (c) 2021 Koding Ninja](./LICENSE)
