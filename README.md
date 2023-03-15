# Everyday Types in TypeScript

### `string, number, boolean`

```
let str: string = "Hello, World";
let num: number = 5;
let bol: boolean = true;
````


### `any`
```
let obj: any = { x: 0 };
obj.foo();
obj();
obj.bar = 100;
obj = "hello";

const n:number = obj;
```


### `function`

- Parameter type annotations
```
function greet (name: string) {
    console.log("Hello, " + name.toUpperCase());
}
great (42); // Error: Argument of type 'number' is not assignable to parameter of type 'string'.
```

- Return type annotations
```
function getFavoriteNumber(): number {
    return 26;
}
```

- Anonymous Functions

const names = ["Alice", "Bob", "Eve"];
```
name.forEach(function (s) {
      console.log(s.toUppercase()); // Error: Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
})
```
```
name.forEach((s) => {
      console.log(s.toUppercase()); // Error: Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
})
```

### `Object Type`
```
function printCoord(pt: { x: number; y: number }) {
    console.log("The coordinate's x value is " + pt.x);
    console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });
```

- Optional Properties
```
function printName(obj: { first: string; last?: string }) {
    // ...
}
// Both OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

```
function printName(obj: { first: string; last?: string }) {
    // Error - might crash if 'obj.last' wasn't provided!
    console.log(obj.last.toUpperCase());

    if (obj.last !== undefined) {
        // OK
        console.log(obj.last.toUpperCase());
    }

    // A safe alternative using modern JavaScript syntax:
    console.log(obj.last?.toUpperCase());
}
```

###  `Union Types`

```
let id: number | string
```

```
console.log(id.toUpperCase()); // Error: Property 'toUpperCase' does not exist on type 'string | number'.
```

```
function printId(id: number | string) {
    if (typeof id === "string") {
        // In this branch, id is of type 'string'
        console.log(id.toUpperCase());
    } else {
        // Here, id is of type 'number'
            console.log(id);
    }
}
```

### `Type Alias`

```
type Point = {
    x: number;
    y: number;
};
const pt: Point;
```

```
type ID = number | string
```

### `Interfaces`

```
interface Point = {
    x: number;
    y: number;
};
const pt: Point;
```

- Differences Between Type Aliases and Interfaces

| Interface | Type |
| ------ | ------ |
| Extending an interface | Extending a type via intersections |
| Adding new fields to an existing interface | A type cannot be changed after being created |


### `Type Assertions`

```
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```
```
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```

### `Literal Types`

```
alignment: "left" | "right" | "center"
```

```
function compare(a: string, b: string): -1 | 0 | 1 {
    return a === b ? 0 : a > b ? 1 : -1;
}
```

- Literal Interface

```
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method);
```

1. You can change the inference by adding a type assertion in either location
```
const req = { url: "https://example.com", method: "GET" as "GET" };
```
2. You can use as const to convert the entire object to be type literals
```
const req = { url: "https://example.com", method: "GET" } as const;
```

### `null and undefined`


```
function liveDangerously(x?: number | null) {
    console.log(x!.toFixed());
}
```

### `Less Common Primitives`

- bigint

```
const oneHundred: bigint = BigInt(100);
```

```
const anotherHundred: bigint = 100n;
```
- symbol

```
const firstName = Symbol("name");
const secondName = Symbol("name");

if (firstName === secondName) {
This condition will always return 'false' since the types 'typeof firstName' and 'typeof secondName' have no overlap.
  // Can't ever happen
}
```
