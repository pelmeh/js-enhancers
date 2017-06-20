# js-enhancers
Collection of JS enhancers

### Object.Tap
Read and modify

```js
{a: 10, b: 30}.tap(console.log) -> {a: 10, b: 30} // and logging

{a: 10, b: 30}.tap(t => t.a = 5) -> {a: 5, b: 30}

[1, 2, 3].tap(t => t.push(4)) -> [1, 2, 3, 4]
```

```js
Object.prototype.tap = function (func) {
	return func(this), this
}
```

### Array.First

```js
[1, 2, 3].first() -> 1
```

```js
Array.prototype.first = function () {
  return this[0]
}
```

### Array.Last

```js
[1, 2, 3].last() -> 3
```

```js
Array.prototype.last = function () {
	return this[this.length - 1]
}
```

### Array.Pusher
Push and return

```js
[1, 2, 3].push(4) -> 3 // it's index
[1, 2, 3].pusher(4) -> [1, 2, 3, 4]
```

```js
Array.prototype.pusher = function (data) {
	this.push(data)
	return this
}
```
or with `Object.Tap` depency
```js
Array.prototype.pusher = function (data) {
	return this.tap(t => t.push(data))
}
```

### Array.Compact
Clear array

```js
[1, null, 3, undefined, 5].compact() -> [1, 3, 5]
```

```js
Array.prototype.compact = function () {
	return this.reduce((newArray, current) => {
		if (current !== undefined && current !== null) newArray.push(current)
		return newArray
	}, [])
}
```
### Number.Times
Repeat `N` times

```js
3..times(i => console.log(i)) -> 1 / 2 / 3
(3).times((i, total) => alert(i)) -> 1 / 2 / 3
```

```js
Number.prototype.times = function (func) {
	for (let i = 0; i < this.valueOf(); i++) func(i, this.valueOf())
}
```
