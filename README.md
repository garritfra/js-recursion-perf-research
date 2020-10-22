# Recursion Performance Research

Executing this recursive fibonacci function takes around 9.5 seconds on my machine, using a traditional approach:

```js
const fib = (n) => {
  if (n == 1) return 0;
  if (n == 2) return 1;
  return fib(n - 1) + fib(n - 2);
};

console.log(fib(45));
```

```sh
➜ time node index.js
701408733
node index.js 9,50s user 0,04s system 99% cpu 9,566 total
```

However, when I wrap the body of the function in another function that gets executed right away, execution drops to 7.5 seconds:

```js
const fib = (n) => {
  return (() => {
    if (n == 1) return 0;
    if (n == 2) return 1;
    return fib(n - 1) + fib(n - 2);
  })();
};

console.log(fib(45));
```

```sh
➜ time node index.js
701408733
node index.js 7,58s user 0,25s system 99% cpu 7,852 total
```

This is a huge speedup (~30%!), but I cannot figure out why wrapping the function would make this difference.

This repo contains resources to help investigate this. A blog post will follow...
