# Calcular Demo

> Simple Calculator demo which performs basic maths using the power of Vue, TypeScript, and our minds.

## Requirements

* Create a calculator that can add, subtract, multiply, and divide. Don't worry about order of operations.
* The calculator should display running history of calculations made. 
* The history should be persistent across calculations.
* Nice to have: the history should persist browser refresh.

## Abstract

> This is based from vue-calculator sample work per [José Salazar](https://codepen.io/jsalazart)
> The example was modified to meet the above requirements and styled so the history looks similar to a running tape.
> There were a number of buggy behaviors in the sample. See test cases for more details.

## Test Cases

1. Upon launching app, ensure the display starts with 0. Ensure it displays the minimum viable operators specified in requirements.
2. Perform a number of random calculations (e.g. 3*3, 15-4, etc) hit = to evaluate each run, confirm the correct maths reported.
3. Assuming previous test cases pass, ensure the running history logs the successful calculations.
4. Nice to have - Ensure the modulus operator ("%") and decimal operator are shown (".")
5. Nice to have - Ensure the C function clears immediate display to 0.
6. Nice to have - Assuming previous test passes, refresh browser, and confirm the running history is still resident.
7. Nice to have - Assuming previous test passes, ensure the AC function clears the immediate and running history areas.
8. Edge case - Hit AC, enter operator without providing number, ensure the display remains unaffected.
9. Edge case - Hit AC, enter some number value followed by an operator (e.g. "*") then immediately click a different operator (e.g. "/"). Expect the operator is replaced (e.g. * becomes /)
10. Edge case - Provide an incomplete expression (e.g. 13 *) then click = to evaluate, confirm no calculation occurred, and nothing logged to running history.

## Build Setup

``` bash
# install dependencies
npm install

# build for development
npm run build

# serve using webpack dev
npm run dev

# clean up dependencies (requires git)
npm run clean
```

## System Dependencies

``` bash
# npm version: 6.9.0
npm --version

# node version: 12.6.0
node --version

# git version: git version 2.20.1 (Apple Git-117)
git --version
```

### References

* [José Salazar's Vue Calculator from CodePen](https://codepen.io/jsalazart/pen/jJWMVw).
* [Installing Node & NPM on a Mac](https://treehouse.github.io/installation-guides/mac/node-mac.html).
* [Using the dev tools for Safari on Mac](https://support.apple.com/guide/safari/use-the-developer-tools-in-the-develop-menu-sfri20948/mac).
* [Microsoft TypeScript Vue Starter](https://github.com/Microsoft/TypeScript-Vue-Starter).
* [John Papa: Vue.js with TypeScript](https://johnpapa.net/vue-typescript/).
