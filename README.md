# a-toolbox

[![NPM Version](http://img.shields.io/npm/v/a-toolbox.svg?style=flat)](https://www.npmjs.org/package/a-toolbox)
[![NPM Downloads](https://img.shields.io/npm/dm/a-toolbox.svg?style=flat)](https://www.npmjs.org/package/a-toolbox)

[![JS Standard Style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

javascript lightweight basic tools for node.js and browser

## Purpose

> "This is my rifle. There are many others like it, but this one is mine."

## Install

````bash
npm i a-toolbox --save
````

## Quick start

```js
const tools = require('a-toolbox')

tools.string.trim('({cut these brackets please)}', ['{', '}', '(', ')'])
// > 'cut these brackets please'

```

modular import

```js
const tools = {
  string: require('a-toolbox/string'),
  fs: require('a-toolbox/fs')
}

```

### On browser

````html
<script src="node_modules/a-toolbox/dist/atoolbox.min.js"></script>
<script>
var data = {
  name: 'Alice',
  year: 2014,
  color: 'purple'
};

var str = '<div>My name is {name} I was born in {year} and my favourite color is {color}</div>{nothing}';
console.log('template:', tools.string.template(str, data));

//> template: <div>My name is Alice I was born in 2014 and my favourite color is purple</div>{nothing}
</script>
````

## API

- [array](#array)
- [fs](#fs)
- [hash](#hash)
- [object](#object)
- [util](#util)
- [random](#random)
- [string](#string)
- [sys](#sys)
- [time](#time)
- [task](#task)
- [event](#event)

### array

#### array.remove(array, item)  
- _array_ \<Array<*>\>  
- _item_ \<*\>  
  

remove an element from array
it removes only the first occurrence  

_Example_

````js
let a = ['js','ruby','python']
tools.array.remove(a, 'ruby')
// > a = ['js','python']
````

#### array.removeAt(array, index)  
- _array_ \<Array<*>\>  
- _index_ \<number\>  
  

remove an element from array at position  

_Example_

````js
let a = [1,2,3]
tools.array.removeAt(a, 0)
// > a = [2,3]
````

#### array.last(array)  
- _array_ \<Array<*>\>  
- _return:_ * last element of the array or undefined  

get last element of array or undefined  

_Example_

````js

tools.array.last([1,2,3])
// > 3
````

#### array.at(array)  
- _array_ \<Array<*>\>  
- _return:_ * nth element of array; if negative, start from end: -1 = last element; undefined if missing  

get nth element of array  

_Example_

````js

tools.array.at([1,2,3], 0)
// > 1
````

#### array.first(array)  
- _array_ \<Array<*>\>  
- _return:_ * first element of the array or undefined  

get first element of array or undefined  

_Example_

````js

tools.array.first([1,2,3])
// > 1
````

#### array.contains(array, item)  
- _array_ \<Array<*>\>  
- _item_ \<*\>  
- _return:_ boolean   

check if array contains an element  

_Example_

````js

tools.array.contains([1,2,3], 1)
// > true
````

#### array.insert(array, index, item)  
- _array_ \<Array<*>\>  
- _index_ \<number\>  
- _item_ \<*\>  
  

insert an item into array at index position  

_Example_

````js
let a = ['john','alice','bob']
tools.array.insert(a, 0, 'mary')
// > a = ['mary', 'john', 'alice', 'bob']
````

#### array.concat(arrays)  
- _arrays_ \<...Array<*>\> to chain 
- _return:_ Array\<*\> chained arrays  

concat arrays  

_Example_

````js

tools.array.concat([0,1,2],[3,4,5])
// > [0,1,2,3,4,5]
````

#### array.empty()  

  

empty array - need to keep references  

_Example_

````js
let a = [0,1,2]
tools.array.empty(a)
// > a = []
````

#### array.add(array, item, [unique=false])  
- _array_ \<Array<*>\>  
- _item_ \<*\>  
- _[unique=false]_ \<boolean\>  
  

push item into array, optionally check if already exists  

_Example_

````js
let a = [0,1,2,3]
tools.array.add(a, 3, true)
// > a = [0,1,2,3]
````

#### array.flat(array)    
- _array_ \<Array<*>\>  
- _return:_ Array\<*\> flatten array  
  

creates a new array with all sub-array elements concatted into it recursively like ``Array.prototype.flatten()``


_Example_

````js
let a = [0,[1,2],[3]] >
tools.array.flat(a)
// > [0,1,2,3]
````

#### array.sortingInsert(array_, item)  
- _array__ \<Array<*>\>  
- _item_ \<*\>  
insert an element in a sorted array, keeping sorted  

_Example_

````js
let a = [0,1,2,10,11,20]
tools.array.sortingInsert(a, 15)
// > a = [0,1,2,10,11,15,20]
````

#### array.binaryIndexOf(array, item)  
- _array_ \<Array<*>\>  
- _item_ \<*\>  

- _return:_ number index of element of -1
like Array.indexOf but perform binary search (array should be sorted)  

_Example_

````js

tools.array.binaryIndexOf([0,1,2,3], 0)
// > 0
````

---

### fs
note: not available on browser

#### fs.exists(path)  
- _path_ \<string\> path 
- _return:_ Promise.\<boolean\> true if file or directory exists

replace deprecated fs.exists  

_Example_

````js

tools.fs.exists('/tmp/file')
// > true
````

#### fs.isFile(path)  
- _path_ \<string\> file path 
- _return:_ Promise.\<boolean\> true if it exists and is a file

_Example_

````js

tools.fs.isFile('/tmp/file')
// > true
````

#### fs.isDirectory(path)  
- _path_ \<string\> dir path 
- _return:_ Promise.\<boolean\> true if it exists and is a dir

_Example_

````js

tools.fs.isDirectory('/tmp')
// > true
````

#### fs.touch(path, [mode=0o666])  
- _path_ \<string\> file path 
- _[mode=0o666]_ \<number\>  
- _return:_ Promise.\<void\>   

create an empty file if not exists  

_Example_

````js

tools.fs.touch('/tmp/touch-me')

````

#### fs.unlink(path, [safe=true])  
- _path_ \<string\> file path 
- _[safe=true]_ \<boolean\> if safe do not throw exception 
- _return:_ Promise.\<void\>   

delete file, optionally in safe mode  

_Example_

````js

tools.fs.unlink('/tmp/file')

````

---

### hash

#### hash.sha256(data)  
- _data_ \<string\> any string 
- _return:_ string sha256 in hex format  

Generate hash using sha256 in hex format  

_Example_

````js

tools.hash.sha256('usk6fgbuygbu6')
// > 'ee42f619919727584b66fe25248ed4bba8e87dcfb3e62a90143ea17ba48df58e'
````


---

### object

#### object.flat(obj)  
- _obj_ \<Object\>  
- _return:_ Object   

flat keys in object  

_Example_

````js

tools.object.flat({ a: { a1: 1, a2: 2 }, b: 3 })
// > { 'a.a1': 1, 'a.a2': 2, 'b': 3 }
````

#### object.merge(a, b)  
- _a_ \<Object\>  
- _b_ \<Object\>  
  

merge b into a  

_Example_

````js
let a = {a:1,b:'ciao'}
tools.object.merge(a, {a:4,c:{d:8,e:9}})
// > a = { a: 4, b: 'ciao', c: { d: 8, e: 9 } }
````

#### object.clone(obj)  
- _obj_ \<Object|Array\> The array or the object to clone 
- _return:_ Object|Array   

Clone an array or an object in input  

_Example_

````js

tools.object.clone({a: 1, b: 'ciao'})
// > {a: 1, b: 'ciao'}
````

#### object.getKeys(obj)  
- _obj_ \<Object\>  
- _return:_ Array\<string\>   

  

_Example_

````js

tools.object.getKeys({a: () => { }, b: 1, c: 'ciao'})
// > ['a','b','c']
````

#### object.inherits(destination, source)  
- _destination_ \<Object\>  
- _source_ \<Object\>  
  

it use ``Object.getOwnPropertyNames`` to inherits child from parent, without prototype  

_Example_

````js
let a = {}
tools.object.inherits(a, {f0:() => { },p1:1,p2:'ciao'})
// > a = {f0: () => { }, p1: 1, p2: 'ciao'}
````

#### object.empty(obj)  
- _obj_ \<Object\>  
  

empty object - need to keep references  

_Example_

````js
let a = {a:0,b:1,c:2,d:[],e:{f:-1}}
tools.object.empty(a)
// > a = {}
````

#### object.raise(flat)  
- _flat_ \<Object\>  
- _return:_ Object   

restore flat object  

_Example_

````js
tools.object.raise({ 'a.a1': 1, 'a.a2': 2, 'b': 3 })
// > { a: { a1: 1, a2: 2 }, b: 3 }
````

#### object.getByFlatKey(obj, fkey)  
- _obj_ \<Object\>  
- _fkey_ \<string\>  
- _return:_ Object   

get value in object using a flat key  

_Example_

````js

tools.object.getByFlatKey({ a: { b: {c: 1} } }, 'a.b.c')
// > 1

tools.object.getByFlatKey({ a: { b: [{c: 1}] } }, 'a.b[0].c')
// > 1
````

#### object.setByFlatKey(obj, fkey, val)  
- _obj_ \<Object\>  
- _fkey_ \<string\>  
- _val_ \<*\>  
  

set value in object using a flat key  

_Example_

````js
let a = {}
tools.object.setByFlatKey(a, 'a.b.c', 1)
// > a = { a: { b: {c: 1} } }

let a = {}
tools.object.setByFlatKey(a, 'a.b[0].c', 1)
// > a = { a: { b: [{c: 1}] } }
````


---

### util

#### util.isSet(val)  
- _val_ \<*\>  
- _return:_ bool   

check if ``val`` is setted, means it's not ``null`` or ``undefined``  


#### util.onBrowser()  

- _return:_ bool   

check if you are on browser or not  



---

### string

#### string.template(str, obj, [remove=false])  
- _str_ \<string\>  
- _obj_ \<Object\>  
- _[remove=false]_ \<boolean\> remove missing placeholders from obj, default false 
- _return:_ string   

replace placeholders inside graph brackets {} with obj dictionary
~ES6 template string without $  

_Example_

````js

tools.string.template('hi {name} how are you?', {name: 'Alice'})
// > 'hi Alice how are you?'
````

#### string.trim(str, cuts)  
- _str_ \<string\>  
- _cuts_ \<Array<string>\>  
- _return:_ string   

trim string  

_Example_

````js

tools.string.trim(' regular trim      ')
// > 'regular trim'
````

#### string.replaceAll(str, from, to)  
- _str_ \<string\>  
- _from_ \<string\>  
- _to_ \<string\>  
- _return:_ string   

_Example_

````js

tools.string.replaceAll('abcadaeafaga', 'a', '')
// > 'bcdefg'
````

#### string.capitalize(str)  
- _str_ \<string\>  
- _return:_ string   

  

_Example_

````js

tools.string.capitalize('alice')
// > 'Alice'
````

#### string.prependMissing(prefix, str)  
- _prefix_ \<string\>  
- _str_ \<string\>  
- _return:_ string   

  

_Example_

````js

tools.string.prependMissing('miss ', 'Alice')
// > 'miss Alice'
````


---

### random

#### random.rnd(max)  
- _max_ \<number\>  
- _return:_ number   

get random int from 0 to max  

_Example_

````js

tools.random.rnd(10)
// > 5
````

#### random.number(min, max)  
- _min_ \<number\>  
- _max_ \<number\>  
- _return:_ number   

get random int from min to max  

_Example_

````js

tools.random.number(10, 20)
// > 11
````

#### random.string([length=8], [set=abcdefghijklmnopqrstuvwxyz])  
- _[length=8]_ \<number\>  
- _[set=abcdefghijklmnopqrstuvwxyz]_ \<Array\>  
- _return:_ string   

get random string  

_Example_

````js

tools.random.string(8)
// > 'ajdsfchakwt'
````

#### random.hex([length=8])  
- _[length=8]_ \<number\>  
- _return:_ string   

get random hex string  

_Example_

````js

tools.random.hex(8)
// > '1bc956bf'
````

#### random.hash(salt)  
- _salt_ \<?string\>  
- _return:_ string   

get random hash string  

_Example_

````js

tools.random.hash()
// > '1f8a690b7366a2323e2d5b045120da7e93896f471f8a690b731f8a690b739ab5'
````

#### random.element(array, not)  
- _array_ \<Array<*>\>  
- _not_ \<Array<*>\>  
- _return:_ * element  

get random element from array  

_Example_

````js

tools.random.element([1,2,3,4,5])
// > 1
````

---

### sys
note: not available on browser

#### sys.isRoot()  

- _return:_ bool is root or not  

check if running user is root  

---

### time

#### time.chrono.set([tag=chrono])  
- _[tag=chrono]_ \<string\>  

start a timer identified by tag  

_Example_

````js

tools.time.chrono.set('query')

````

#### time.chrono.reset([tag=chrono])  
- _[tag=chrono]_ \<string\>  

reset the timer identified by tag  

_Example_

````js

tools.time.chrono.reset('query')

````

#### time.chrono.clear([tag=chrono])  
- _[tag=chrono]_ \<string\>  

discard the timer identified by tag  

_Example_

````js

tools.time.chrono.clear('query')

````

#### time.chrono.get([tag=chrono])  
- _[tag=chrono]_ \<string\>  
- _return:_ number ms

get the timer in ms from start (or reset) identified by tag  

_Example_

````js

tools.time.chrono.get('query')
// > 11
````

#### time.gc()  

clear timers (if you care about memory)  

---

### task

#### class task.Worker(options)  
- _options_ \<Object\>  
- _options.done_ \<function\> callback when all tasks are completed 
simple parallel tasks manager  

_Example_

````js

const tasks = new tools.task.Worker({done: () => { console.log('well done') }})

const _asyncOperationTimeout = [500, 1000, 200, 1500, 100];

for (const i in _asyncOperationTimeout) {
  _tasks.todo('task#' + i);
}

for (const i in _asyncOperationTimeout) {
  setTimeout(function (i) {
    return function () {
      console.log('done task #', i);
      _tasks.done('task#' + i);
    };
  }(i), _asyncOperationTimeout[i]);
}

````

#### Worker.todo()  

add task  

_Example_

````js

tasks.todo('task#1')

````

#### Worker.done()  

declare task it's done  

_Example_

````js

tasks.todo('task#1')

````

---

### event

#### class event.Emitter()  
simple event emitter  

_Example_

````js

const emitter = new tools.event.Emitter()

emitter.on('event#0', (value0, value1) => {
  console.log('event #0 happened with', value0, value1)
})

emitter.once('event#0', (value0, value1) => {
  console.log('event #0 happened (once) with', value0, value1)
})

emitter.emit('event#0', 1, 2)
emitter.emit('event#0', 3, 4)

emitter.off('event#0')

````

#### Emitter.emit(name, ...values)   
- _name_ \<string\> event name  
- _...values_ \<*\> values to pass to the event listener  

emit an event  

_Example_

````js

event.emit('event#0', 'a value', 99, {another: 'VALUE'})

````

#### Emitter.on(name, callback)   
- _name_ \<string\> event name  
- _callback_ \<function\> 

listen to an event  

_Example_

````js

emitter.on('event#0', (value0, value1) => {
  console.log('event #0 happened (once) with', value0, value1)
})

````

#### Emitter.once(name, callback)   
- _name_ \<string\> event name  
- _callback_ \<function\> 

listen to an event only once  

_Example_

````js

emitter.once('event#0', (value0, value1) => {
  console.log('event #0 happened (once) with', value0, value1)
})

````

#### Emitter.off(name)   
- _name_ \<string\> event name  

stop listening to an event  

_Example_

````js

emitter.off('event#0')

````

---



## Changelog

v. 1.7.2

- add ``object.getByFlatKey`` support also Array

v. 1.7.1

- add ``fs.isFile`` and ``fs.isDirectory``

v. 1.6.2

- ``fs.exists`` return true on files and directories, instead of only files

v. 1.5.1

- ``string.template`` support multi-level syntax object

v. 1.5.1

- ``object.setByFlatKey`` support also Array

v. 1.5.0

- add ``event.Emitter`` (simple event emitter, for browser)

v. 1.2.0

- use [hash.js](https://github.com/indutny/hash.js) instead of ``crypto`` (for browser)

v. 1.0.0

- general review
- modular loader
- browser version

---

## TODO

- [ ] string.caseCamel, string.casePascal
- [ ] object.walk test, doc
- [ ] travis CI / node, browser
- [ ] coverage badge / coverage 100%

---

## License

The MIT License (MIT)

Copyright (c) 2015-2019, [braces lab](https://braceslab.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
