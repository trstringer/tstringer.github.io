---
layout: post
title:  "Pattern Path Matching in JavaScript"
date:   2016-08-21 22:00
categories: javascript 
---
There are many super cool problems that you can solve with code, and one of the common ones is pattern path matching.  Here's what I mean...

```
a  a  b  b  b  a
a  a  b  b  a  b
a  a  a  a  b  b
b  b  a  a  b  b
a  b  a  a  b  a
b  b  b  a  a  a
```

With this given pattern, the challenge is to go from the upper right corner to the bottem left corner, but the catch is that the elements should only be traversed to the right or down (no diagonal).  And also, you can only travel through elements of `a` and not `b` (those would be "blockers").  So the solution should look like this drawn out...

```
a* a  b  b  b  a
a* a  b  b  a  b
a* a* a* a  b  b
b  b  a* a  b  b
a  b  a* a* b  a
b  b  b  a* a* a*
```

As you can see here, the desired path is marked by `*`.  Here is a simple function that recursively solves this problem...

```javascript
function findPath(patternMap, position, size) {
  if (position[0] == size - 1 && position[1] == size - 1) {
    return [[size - 1, size - 1]];
  }

  const x = position[0];
  const y = position[1];

  if (x + 1 < size && patternMap[x + 1][y] === 'a') {
    const down = findPath(patternMap, [x + 1, y], size);
    if (down) {
      return [[x, y], ...down];
    }
  }

  if (y + 1 < size && patternMap[x][y + 1] === 'a') {
    const right = findPath(patternMap, [x, y + 1], size);
    if (right) {
      return [[x, y], ...right];
    }
  }
}

const patternMap = [
    ['a', 'a', 'b', 'b', 'b', 'a'],
    ['a', 'a', 'b', 'b', 'a', 'b'],
    ['a', 'a', 'a', 'a', 'b', 'b'],
    ['b', 'b', 'a', 'a', 'b', 'b'],
    ['a', 'b', 'a', 'a', 'b', 'a'],
    ['b', 'b', 'b', 'a', 'a', 'a']
  ];

const path = findPath(patternMap, [0, 0], patternMap.length);

console.log(path);
```

The output that you should get from this should be the following...

```
[ [ 0, 0 ],
  [ 1, 0 ],
  [ 2, 0 ],
  [ 2, 1 ],
  [ 2, 2 ],
  [ 3, 2 ],
  [ 4, 2 ],
  [ 4, 3 ],
  [ 5, 3 ],
  [ 5, 4 ],
  [ 5, 5 ] ]
```

Beauty through recursion!  Enjoy!
