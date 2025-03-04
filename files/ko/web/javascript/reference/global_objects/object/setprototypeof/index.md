---
title: Object.setPrototypeOf()
slug: Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf
translation_of: Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf
browser-compat: javascript.builtins.Object.setPrototypeOf
---
{{JSRef}}

Object.setPrototypeOf() 메소드는 지정된 객체의 프로토타입 (즉, 내부 \[\[Prototype]] 프로퍼티)을 다른 객체 또는 {{jsxref("null")}} 로 설정합니다.

> **경고:** Changing the `[[Prototype]]` of an object is, by the nature of how modern JavaScript engines optimize property accesses, a very slow operation, in **_every_** browser and JavaScript engine. The effects on performance of altering inheritance are subtle and far-flung, and are not limited to simply the time spent in `obj.__proto__ = ...` statement, but may extend to **_any_** code that has access to **_any_** object whose `[[Prototype]]` has been altered. If you care about performance you should avoid setting the `[[Prototype]]` of an object. Instead, create a new object with the desired `[[Prototype]]` using {{jsxref("Object.create()")}}.

## Syntax

    Object.setPrototypeOf(obj, prototype);

### Parameters

- `obj`
  - : 프로토타입을 설정을 가지는 객체
- `prototype`
  - : 객체의 새로운 프로토 타입 (객체 or {{jsxref("null")}}).

### Return value

지정된 객체

## Description

만일 프로토타입이 변경될 객체가 {{jsxref("Object.isExtensible()")}} 에 의해서 non-extensible 하다면, {{jsxref("TypeError")}} 예외처리를 해라. 만일 프로토타입 파라미터가 객체가 아니거나 {{jsxref("null")}} (i.e., number, string, boolean, {{jsxref("undefined")}}) 인 경우가 아니라면 어떠한 작업도 하지마라. 이 방법을 통해서 객제의 프로토타입이 새로운 값으로 변경될 것이다.

Object.setPrototypeOf는 ECMAScript 2015 스펙으로 규정되어 있다. 해당 메소드는 일반적으로 객체의 프로토타입과 논쟁이 되는 {{jsxref("Object.prototype.__proto__")}} 프로퍼티를 설정하는 적절한 방법으로 고려된다.

Examples

```js
var dict = Object.setPrototypeOf({}, null);
```

## Polyfill

예전 버전의 프로퍼티 {{jsxref("Object.prototype.__proto__")}} 를 사용한다면, 우리는 쉽게 Object.setPrototypeOf 가 쉽게 정의 할수 있다.

```js
// Only works in Chrome and FireFox, does not work in IE:
Object.setPrototypeOf = Object.setPrototypeOf || function(obj, proto) {
  obj.__proto__ = proto;
  return obj;
}
```

## Appending Prototype Chains

`Object.getPrototypeOf()` and {{jsxref("Object.proto", "Object.prototype.__proto__")}} 의 결합은 새로운 프로토타입 오브젝트에 전반적인 프로토타입 Chain을 설정하도록 할수 있다.

```js
/**
*** Object.appendChain(@object, @prototype)
*
* Appends the first non-native prototype of a chain to a new prototype.
* Returns @object (if it was a primitive value it will transformed into an object).
*
*** Object.appendChain(@object [, "@arg_name_1", "@arg_name_2", "@arg_name_3", "..."], "@function_body")
*** Object.appendChain(@object [, "@arg_name_1, @arg_name_2, @arg_name_3, ..."], "@function_body")
*
* Appends the first non-native prototype of a chain to the native Function.prototype object, then appends a
* new Function(["@arg"(s)], "@function_body") to that chain.
* Returns the function.
*
**/

Object.appendChain = function(oChain, oProto) {
  if (arguments.length < 2) {
    throw new TypeError('Object.appendChain - Not enough arguments');
  }
  if (typeof oProto !== 'object' && typeof oProto !== 'string') {
    throw new TypeError('second argument to Object.appendChain must be an object or a string');
  }

  var oNewProto = oProto,
      oReturn = o2nd = oLast = oChain instanceof this ? oChain : new oChain.constructor(oChain);

  for (var o1st = this.getPrototypeOf(o2nd);
    o1st !== Object.prototype && o1st !== Function.prototype;
    o1st = this.getPrototypeOf(o2nd)
  ) {
    o2nd = o1st;
  }

  if (oProto.constructor === String) {
    oNewProto = Function.prototype;
    oReturn = Function.apply(null, Array.prototype.slice.call(arguments, 1));
    this.setPrototypeOf(oReturn, oLast);
  }

  this.setPrototypeOf(o2nd, oNewProto);
  return oReturn;
}
```

### Usage

#### First example: 프로토타입에 Chain 설정하기

```js
function Mammal() {
  this.isMammal = 'yes';
}

function MammalSpecies(sMammalSpecies) {
  this.species = sMammalSpecies;
}

MammalSpecies.prototype = new Mammal();
MammalSpecies.prototype.constructor = MammalSpecies;

var oCat = new MammalSpecies('Felis');

console.log(oCat.isMammal); // 'yes'

function Animal() {
  this.breathing = 'yes';
}

Object.appendChain(oCat, new Animal());

console.log(oCat.breathing); // 'yes'
```

#### Second example: 객체 Constructor의 인스턴스에 존재하는 원래 값을 변경 및 해당 객체 프로토타입에 Chain 설정하기

```js
function MySymbol() {
  this.isSymbol = 'yes';
}

var nPrime = 17;

console.log(typeof nPrime); // 'number'

var oPrime = Object.appendChain(nPrime, new MySymbol());

console.log(oPrime); // '17'
console.log(oPrime.isSymbol); // 'yes'
console.log(typeof oPrime); // 'object'
```

#### Third example: Function.prototype객체에 Chain을 설정하고 그 Chain에 새로운 함수를 설정하기

```js
function Person(sName) {
  this.identity = sName;
}

var george = Object.appendChain(new Person('George'),
                                'console.log("Hello guys!!");');

console.log(george.identity); // 'George'
george(); // 'Hello guys!!'
```

## 명세

{{Specifications}}

## 브라우저 호환성

{{Compat}}

## See also

- {{jsxref("Reflect.setPrototypeOf()")}}
- {{jsxref("Object.prototype.isPrototypeOf()")}}
- {{jsxref("Object.getPrototypeOf()")}}
- {{jsxref("Object.prototype.__proto__")}}
