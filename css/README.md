# How we use BEM with Sass modules

There are legends, tells that you don't need BEM, if you use
CSS modules, but we need convention in our company. This convention
is written below.

We will not use the 'all' BEM, because BEM is not only about
how to write CSS. BEM is methodology, that also tells how to
structure your file system, etc. Anyway, we will use only the naming convention
of BEM, but with our corrections.

BEM stands for "Block-Element-Modifier".  

## Block
**Block** is the reusable chunk of
code. The block name describes its purpose ('What is it?' - `menu` or `button`).
- The block shouldn't influence its environment, meaning you shouldn't set the 
  external geometry (margin) or positioning for the block.
- You also shouldn't use CSS tag or ID selectors when using BEM.  

```
<!-- Correct. The `error` block is semantically meaningful -->
<div class="error"></div>

<!-- Incorrect. It describes the appearance -->
<div class="redText"></div>
```
- Blocks can be nested in each other.
- You can have any number of nesting levels.
```
<!-- `header` block -->
<header class="header">
    <!-- Nested `logo` block -->
    <div class="logo"></div>

    <!-- Nested `searchForm` block -->
    <form class="searchForm"></form>
</header>
```

## Element
**Element** is a composite part of a block that can't be used separately from it.
- The element name describes its purpose ("What is this?" — `item`, `text`, etc.), 
not its state ("What type, or what does it look like?" — `red`, `big`, etc.).
- The structure of an element's full name is `blockName_elementName`.
  The element name is separated from the block name with an underscore (_).
```
  <!-- `searchForm` block -->
  <form class="searchForm">
      <!-- `input` element in the `searchForm` block -->
      <input class="searchForm_input">

      <!-- `button` element in the `searchForm` block -->
      <button class="searchForm_button">Search</button>
  </form>
```

- Elements can be nested inside each other.
- You can have any number of nesting levels.
- An element is always part of a block, not another element. This means that element 
names can't define a hierarchy such as block_elem1_elem2.
  
```
  <!--
    Correct. The structure of the full element name follows the pattern:
    `blockName_elementName`
  -->
  <form class="searchForm">
      <div class="searchForm_content">
          <input class="searchForm_input">

          <button class="searchForm_button">Search</button>
      </div>
  </form>

  <!--
      Incorrect. The structure of the full element name doesn't follow the pattern:
      `blockName_elementName`
  -->
  <form class="searchForm">
      <div class="searchForm_content">
          <!-- Recommended: `searchForm_input` or `searchForm_contentInput` -->
          <input class="searchForm_content_input">

          <!-- Recommended: `searchForm_button` or `searchForm_contentButton` -->
          <button class="searchForm_content_button">Search</button>
      </div>
  </form>
```

## Modifier
**Modifier** An entity that defines the appearance, state, or behavior of a block or element.
- The modifier name describes its appearance ("What size?" or "Which theme?" and so on — `sizeS` 
  or `themeIslands`), its state ("How is it different from the others?" — `disabled`, `focused`, etc.) 
  and its behavior ("How does it behave?" or "How does it respond to the user?" — such 
  as `directionsLeftTop`).
- The modifier name is separated from the block or element name by double underscore (__).
- A modifier can't be used alone. From the BEM perspective, a modifier can't be used in isolation 
  from the modified block or element. A modifier should change the appearance, behavior, or state 
  of the entity, not replace it.
```
  <!--
      Correct. The `searchForm` block has the `theme` modifier with
      the value `islands`
  -->
  <form class="searchForm searchForm__themeIslands">
      <input class="searchForm_input">

      <button class="searchForm_button">Search</button>
  </form>

  <!-- Incorrect. The modified class `searchForm` is missing -->
  <form class="searchForm__themeIslands">
      <input class="searchForm_input">

      <button class="searchForm_button">Search</button>
  </form>
```
The div above is the reusable Block that has styles class 'blockName'. Block
doesn't have to have elements inside it, Block could be solid.

> **Note** that we use camelCase for class names, not kebab-case or snake_case

---
When we were discussing using BEM in our projects, there was a question about
upper container. As we use frameworks and component approach to writing apps,
we need some agreement on how to name class of the main tag in the component.
Components could be just `div` with text in it or a bit complex, but still
don't have more than one tag. Name the only class with the name of the component
is bad idea, because component could be very long, and have such long class name
in simple component don't look good. And we decided to name the upper tag's (first one)
class name just `container`. The idea is that first tag is the container of 
component's elements. Container, as BEM block, could be empty. The second tag's
class name will not be `container_blockName` or `container_elementName`, it will
be just `blockName`. Any element that defined in container is a block:

```
<div className="container">
    <!-- If it is a block -->
    <div className="blockName">
        <div className="blockName__elementName"></div>
    </div>
    
    <!-- If it is an element -->
    <div className="elementName"></div>
</div>
```

---
Remember that every member of Staq can offer a correction to this convention
or even brand new convention. You just need to explain why we need it.
---
[Shamil Khashaev](https://github.com/skhashaev)
