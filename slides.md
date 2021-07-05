---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
routerMode: hash
---

# Array-find-from-last

Wenlu Wang, Daniel Rosenwasser, Microsoft Corporation

<div class="abs-br m-6 flex gap-2">
  <span class=".text-sm">
    Powered by <a href="https://github.com/slidevjs/slidev">slidev</a>
  </span>
</div>

---

# Status

- 🔨 **Github Repo** - https://github.com/tc39/proposal-array-find-from-last
- 📝 **Proposed spec text** - https://tc39.es/proposal-array-find-from-last/
- 🧑 **Path to stage-3** - https://github.com/tc39/proposal-array-find-from-last/issues/36
- 📚 **Implementations** - https://github.com/tc39/proposal-array-find-from-last/issues/37
- 👀 **What's Next** - Seeking for stage-3

---

# Updates

## No major changes.

- [**Use _k_ insted of _idx_**](https://github.com/tc39/proposal-array-find-from-last/pull/38) - Wenlu Wang
- [**Remove phrasing for arity on findLastIndex**](https://github.com/tc39/proposal-array-find-from-last/pull/39) - Daniel Rosenwasser
- [**Add explicit algorithm steps for TypedArrays**](https://github.com/tc39/proposal-array-find-from-last/pull/45) - Daniel Rosenwasser

---

# Spec text - Array.prototype.findLast

<div class="spec">
  <p class="h1">
    <b>
      Array.prototype.findLast ( <span class="var">predicate</span> [ , <span class="var">thisArg</span> ] )
    </b>
  </p>
  <ol>
    <li>
      Let <span class="var">O</span> be ? <span class="xref">ToObject</span>(<span class="val">this</span> value).
    </li>
    <li>
      Let <span class="var">len</span> be ? <span class="xref">LengthOfArrayLike</span>(<span class="var">O</span>).
    </li>
    <li>
      If <span class="xref">IsCallable</span>(<span class="var">predicate</span>) is <span class="val">false</span>, throw a <span class="val">TypeError</span> exception.
    </li>
    <li>
      Let <span class="var">k</span> be <span class="var">len</span> - 1.
    </li>
    <li>
      <span>Repeat, while <span class="var">k</span> ≥ 0</span>,
      <ol class="sublist">
        <li>
          Let <span class="var">Pk</span> be ! <span class="xref">ToString</span>(<span class="xref">𝔽</span>(<span class="var">k</span>)).
        </li>
        <li>
          Let <span class="var">kValue</span> be ? <span class="xref">Get</span>(<span class="var">O</span>, <span class="var">Pk</span>).
        </li>
        <li>
          Let <span class="var">testResult</span> be ! <span class="xref">ToBoolean</span>(? <span class="xref">Call</span>(<span class="var">predicate</span>, <span class="var">thisArg</span>, « <span class="var">kValue</span>, <span class="xref">𝔽</span>(<span class="var">k</span>), <span class="var">O</span> »)).
        </li>
        <li>
          If <span class="var">testResult</span> is <span class="val">true</span>, return <span class="var">kValue</span>.
        </li>
        <li>
          Set <span class="var">k</span> to <span class="var">k</span> - <span>1</span>.
        </li>
      </ol>
    </li>
    <li>
      Return <span class="val">undefined</span>.
    </li>
  </ol>
</div>

<style>

.spec {
  font-family: Cambria, Palatino Linotype, Palatino, Liberation Serif, serif;
}

.var {
  color: #2aa198;
  transition: background-color 0.25s ease;
}

.xref {
  color: #206ca7;
  text-decoration: none;
}

.val {
      font-weight: bold;
}

.sublist {
  list-style-type: lower-alpha;
}

</style>

---

# Spec text - Array.prototype.findLastIndex

<div class="spec">
  <p class="h1">
    <b>
      Array.prototype.findLastIndex ( <span class="var">predicate</span> [ , <span class="var">thisArg</span> ] )
    </b>
  </p>
  <ol>
    <li>
      Let <span class="var">O</span> be ? <span class="xref">ToObject</span>(<span class="val">this</span> value).
    </li>
    <li>
      Let <span class="var">len</span> be ? <span class="xref">LengthOfArrayLike</span>(<span class="var">O</span>).
    </li>
    <li>
      If <span class="xref">IsCallable</span>(<span class="var">predicate</span>) is <span class="val">false</span>, throw a <span class="val">TypeError</span> exception.
    </li>
    <li>
      Let <span class="var">k</span> be <span class="var">len</span> - 1.
    </li>
    <li>
      <span>Repeat, while <span class="var">k</span> ≥ 0</span>,
      <ol class="sublist">
        <li>
          Let <span class="var">Pk</span> be ! <span class="xref">ToString</span>(<span class="xref">𝔽</span>(<span class="var">k</span>)).
        </li>
        <li>
          Let <span class="var">kValue</span> be ? <span class="xref">Get</span>(<span class="var">O</span>, <span class="var">Pk</span>).
        </li>
        <li>
          Let <span class="var">testResult</span> be ! <span class="xref">ToBoolean</span>(? <span class="xref">Call</span>(<span class="var">predicate</span>, <span class="var">thisArg</span>, « <span class="var">kValue</span>, <span class="xref">𝔽</span>(<span class="var">k</span>), <span class="var">O</span> »)).
        </li>
        <li>
          If <span class="var">testResult</span> is <span class="val">true</span>, return <span class="xref">𝔽</span> ( <span class="var">k</span>).
        </li>
        <li>
          Set <span class="var">k</span> to <span class="var">k</span> - <span>1</span><span class="sub">𝔽</span>.
        </li>
      </ol>
    </li>
    <li>
      Return <span class="val">-1</span>.
    </li>
  </ol>
</div>

<style>

.spec {
  font-family: Cambria, Palatino Linotype, Palatino, Liberation Serif, serif;
}

.var {
  color: #2aa198;
  transition: background-color 0.25s ease;
}

.xref {
  color: #206ca7;
  text-decoration: none;
}

.val {
  font-weight: bold;
}

.sublist {
  list-style-type: lower-alpha;
}

.sub {
  vertical-align: sub;
  font-size: smaller;
}

</style>

---

# Spec text - %TypedArray%.prototype.findLast

<div class="spec">
  <p class="h1">
    <b>
      %TypedArray%.prototype.findLast ( <span class="var">predicate</span> [ , <span class="var">thisArg</span> ] )
    </b>
  </p>
  <ol>
    <li>
      Let <span class="var">O</span> be ? <span class="xref">ToObject</span>(<span class="val">this</span> value).
    </li>
    <li>
      Perform ? <span class="xref">ValidateTypedArray</span>(<span class="var">O</span>).
    </li>
    <li>
      Let <span class="var">len</span> be ? <span class="var">O</span>.[[ArrayLength]].
    </li>
    <li>
      If <span class="xref">IsCallable</span>(<span class="var">predicate</span>) is <span class="val">false</span>, throw a <span class="val">TypeError</span> exception.
    </li>
    <li>
      Let <span class="var">k</span> be <span class="var">len</span> - 1.
    </li>
    <li>
      <span>Repeat, while <span class="var">k</span> ≥ 0</span>,
      <ol class="sublist">
        <li>
          Let <span class="var">Pk</span> be ! <span class="xref">ToString</span>(<span class="xref">𝔽</span>(<span class="var">k</span>)).
        </li>
        <li>
          Let <span class="var">kValue</span> be ? <span class="xref">Get</span>(<span class="var">O</span>, <span class="var">Pk</span>).
        </li>
        <li>
          Let <span class="var">testResult</span> be ! <span class="xref">ToBoolean</span>(? <span class="xref">Call</span>(<span class="var">predicate</span>, <span class="var">thisArg</span>, « <span class="var">kValue</span>, <span class="xref">𝔽</span>(<span class="var">k</span>), <span class="var">O</span> »)).
        </li>
        <li>
          If <span class="var">testResult</span> is <span class="val">true</span>, return <span class="var">kValue</span>.
        </li>
        <li>
          Set <span class="var">k</span> to <span class="var">k</span> - <span>1</span>.
        </li>
      </ol>
    </li>
    <li>
      Return <span class="val">undefined</span>.
    </li>
  </ol>
</div>

<style>

.spec {
  font-family: Cambria, Palatino Linotype, Palatino, Liberation Serif, serif;
}

.var {
  color: #2aa198;
  transition: background-color 0.25s ease;
}

.xref {
  color: #206ca7;
  text-decoration: none;
}

.val {
  font-weight: bold;
}

.sublist {
  list-style-type: lower-alpha;
}

</style>

---

# Spec text - %TypedArray%.prototype.findLastIndex

<div class="spec">
  <p class="h1">
    <b>
      %TypedArray%.prototype.findLastIndex ( <span class="var">predicate</span> [ , <span class="var">thisArg</span> ] )
    </b>
  </p>
  <ol>
    <li>
      Let <span class="var">O</span> be ? <span class="xref">ToObject</span>(<span class="val">this</span> value).
    </li>
    <li>
      Perform ? <span class="xref">ValidateTypedArray</span>(<span class="var">O</span>).
    </li>
    <li>
      Let <span class="var">len</span> be ? <span class="var">O</span>.[[ArrayLength]].
    </li>
    <li>
      If <span class="xref">IsCallable</span>(<span class="var">predicate</span>) is <span class="val">false</span>, throw a <span class="val">TypeError</span> exception.
    </li>
    <li>
      Let <span class="var">k</span> be <span class="var">len</span> - 1.
    </li>
    <li>
      <span>Repeat, while <span class="var">k</span> ≥ 0</span>,
      <ol class="sublist">
        <li>
          Let <span class="var">Pk</span> be ! <span class="xref">ToString</span>(<span class="xref">𝔽</span>(<span class="var">k</span>)).
        </li>
        <li>
          Let <span class="var">kValue</span> be ? <span class="xref">Get</span>(<span class="var">O</span>, <span class="var">Pk</span>).
        </li>
        <li>
          Let <span class="var">testResult</span> be ! <span class="xref">ToBoolean</span>(? <span class="xref">Call</span>(<span class="var">predicate</span>, <span class="var">thisArg</span>, « <span class="var">kValue</span>, <span class="xref">𝔽</span>(<span class="var">k</span>), <span class="var">O</span> »)).
        </li>
        <li>
          If <span class="var">testResult</span> is <span class="val">true</span>, return <span class="xref">𝔽</span> ( <span class="var">k</span>).
        </li>
        <li>
          Set <span class="var">k</span> to <span class="var">k</span> - <span>1</span><span class="sub">𝔽</span>.
        </li>
      </ol>
    </li>
    <li>
      Return <span class="val">-1</span>.
    </li>
  </ol>
</div>

<style>

.spec {
  font-family: Cambria, Palatino Linotype, Palatino, Liberation Serif, serif;
}

.var {
  color: #2aa198;
  transition: background-color 0.25s ease;
}

.xref {
  color: #206ca7;
  text-decoration: none;
}

.val {
  font-weight: bold;
}

.sublist {
  list-style-type: lower-alpha;
}

.sub {
  vertical-align: sub;
  font-size: smaller;
}

</style>

---

# Spec text - Array.prototype [@@unscopables]

<div class="spec">
  <ol>
    <li>
      Let <span class="var">unscopableList</span> be OrdinaryObjectCreate(<span class="val">null</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"copyWithin"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"entries"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"fill"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"find"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"findIndex"</span>, <span class="val">true</span>).
    </li>
    <li>
      <span class="ins">
        Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"findLast"</span>, <span class="val">true</span>).
      </span>
    </li>
    <li>
      <span class="ins">
        Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"findLastIndex"</span>, <span class="val">true</span>).
      </span>
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"flat"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"flatMap"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"includes"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"keys"</span>, <span class="val">true</span>).
    </li>
    <li>
      Perform ! <span class="xref">CreateDataPropertyOrThrow</span>(<span class="var">unscopableList</span>, <span class="val">"values"</span>, <span class="val">true</span>).
    </li>
  </ol>
</div>

<style>

.spec {
  font-family: Cambria, Palatino Linotype, Palatino, Liberation Serif, serif;
}

.var {
  color: #2aa198;
  transition: background-color 0.25s ease;
}

.xref {
  color: #206ca7;
  text-decoration: none;
}

.val {
  font-weight: bold;
}

.sublist {
  list-style-type: lower-alpha;
}

.sub {
  vertical-align: sub;
  font-size: smaller;
}

.ins {
  background-color: #e0f8e0;
  text-decoration: none;
  border-bottom: 1px solid #396;
}

</style>

---

# Path to stage-3

**Thanks to everyone!**

- Complete spec text
  - ✔️ Wenlu Wang
  - ✔️ Daniel Rosenwasser
- Reviewers signed off
  - ✔️ Jordan Harband
  - ✔️ Leo Balter 
  - ✔️ Yulia Startsev
- Editors signed off
  - ✔️ Shu-yu Guo

---

# Implementations

- [**Core-js**](https://github.com/zloirock/core-js/blob/master/CHANGELOG.md#3100---20210331) 
- [**ChakraCore (behind flag)**](https://github.com/chakra-core/ChakraCore/pull/6653)

---

# Compatibility

## Appreciate if someone could help for the investigation!

---
layout: center
class: text-center
---

# Thanks

---
layout: center
class: text-center
---

# Stage-3 ?

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>
