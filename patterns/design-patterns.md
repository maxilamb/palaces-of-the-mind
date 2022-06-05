# JavaScript Design Patterns

#### Builder

`Позволяет создавать различные варианты объекта, избегая загрязнения конструктора. Полезно, когда может быть несколько вариантов объекта. Или когда есть много шагов, связанных с созданием объекта.`

> OOP

```js

class DataTransform {
  constructor() {
    this.data = "";
  }

  toCSV() {
    this.data = "csv";
    return this;
  }

  toJSON() {
    this.data = "json";
    return this;
  }

  toBinary() {
    this.data = "binary";
    return this;
  }

  build() {
    return this.data;
  }
}

const transformer = new DataTransform().toCSV().toBinary().build();

console.log("transformer", transformer);

```

> FP

```js
function builder(counter = 0) {
  this.count = counter;

  this.increment = () => {
    this.count += 1;
    return this;
  };

  this.decrement = () => {
    this.count -= 1;
    return this;
  };

  this.reset = () => {
    this.count = 0;
    return this;
  };

  this.build = () => {
    return this.count;
  };
}

const count = new builder().increment().increment().increment().build();

console.log(count);

```
