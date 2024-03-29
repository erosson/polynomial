[![npm version](https://badge.fury.io/js/@erosson%2Fpolynomial.svg)](https://www.npmjs.com/package/@erosson/polynomial)
[![cdn usage](https://data.jsdelivr.com/v1/package/npm/@erosson/polynomial/badge)](https://www.jsdelivr.com/package/npm/@erosson/polynomial)

Polynomials for Typescript. Also, implements [Swarm Simulator](https://www.swarmsim.com)-style polynomial unit production.

Basic polynomials:

```ts
import {Polynomial} from "@erosson/polynomial"

const p = Polynomial.parse([3,2,1])
p  // [3, 2, 1]
p.toString()  // "t^2 + 2 t + 3"

p.add(Polynomial.parse([1, 2, 3]))  // [4, 4, 4]
p.mul(5)  // [15, 10, 5]
p.evaluate(0)  // 3
p.evaluate(1)  // 6
p.evaluate(2)  // 11
```

Other number formats are supported, like [Decimal.js](https://mikemcl.github.io/decimal.js/):

```ts
import {Polynomial, decimalNumberOps, nativeNumberOps} from "@erosson/polynomial"
import Decimal from "decimal.js"

const p1 = Polynomial.parse([3, 2, 1], nativeNumberOps)
p1.toString()  // "t^2 + 2 t + 3"

const p2 = Polynomial.parse([new Decimal(3), new Decimal(2), new Decimal(1)], decimalNumberOps(Decimal))
p2.toString()  // "t^2 + 2 t + 3"
```

Construct polynomials describing a unit production graph, like [Swarm Simulator](https://www.swarmsim.com):

```ts
import {Production} from "@erosson/polynomial"

const vertices = new Map([['drone', 3], ['meat', 2]])
const edges = [{from: 'drone', to: 'meat', each: 5}]
const polys = Production.simpleGraphToPolynomials(vertices, edges)
polys.get('drone').toString()  // "3"
polys.get('meat').toString()  // "2 + 15 t"
```

## Usage

In the browser, pick an import style:

```html
<script type="module">
    import {Polynomial} from "https://esm.run/@erosson/polynomial@latest"
    ...
</script>
```

```html
<script src="https://cdn.jsdelivr.net/npm/@erosson/polynomial@latest"></script>
<script>
    // it's now at `Polynomial` or `window.Polynomial`
</script>
```

In Node, to install via NPM:

`npm install --save https://github.com/erosson/polynomial`

In Node, to install via Yarn:

`yarn add https://github.com/erosson/polynomial`

Once installed, pick an import style:

```ts
import {Polynomial} from "@erosson/polynomial"
```

```ts
const {Polynomial} = require("@erosson/polynomial");
```