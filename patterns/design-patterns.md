# Паттерны проектирования

Паттерн проектирования — это часто встречающееся решение определённой проблемы при проектировании архитектуры программ.

* **Порождающие** паттерны беспокоятся о гибком создании объектов без внесения в программу лишних зависимостей.
* **Структурные** паттерны показывают различные способы построения связей между объектами.
* **Поведенческие** паттерны заботятся об эффективной коммуникации между объектами.

## Пораждающие паттерны

### Фабричный метод

Фабричный метод — определяет общий интерфейс для создания объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.

```js

const car = (price, color) => ({
    price,
    color
});

const ship = (price, color) => ({
    price,
    color,
    weight: '3m',
    height: '2m'
});

// factory method
const factoryCar = (type) => {
    const carMap = {
        bmw: car(1000, 'red'),
        audi: car(1000, 'red'),
    }

    return carMap[type];
}

// factory method
const factoryShip = (type) => {
    const shipMap = {
        shipe: ship(10000, 'green'),
    }

    return carMap[type];
}

```

### Абстрактная фабрика

Абстрактная фабрика —  позволяет создавать семейства связанных объектов, не привязываясь к конкретным классам создаваемых объектов.

```js 

const shop = (transportType) => {
    const transportFactoryMap = {
        car: factoryCar,
        ship: factoryShip
    }

    return transportFactoryMap[type];
}

const transport = shop('car');
const transport2 = shop('ship');


const bmw = transport("bmw");
const shipe = transport2("ship");

```

### Строитель (Builder)

Строитель —  позволяет создавать сложные объекты пошагово. Строитель даёт возможность использовать один и тот же код строительства для получения разных представлений объектов.

```js

function CarBuilder() {
  let car = {};

  this.addDoor = (value) => {
    car = {
      ...car,
      door: value
    };
    return this;
  };

  this.addWheel = (value) => {
    car = {
      ...car,
      wheel: value
    };
    return this;
  };

  this.build = () => {
    return car;
  };
}

const car = new CarBuilder().addDoor(2).addWheel(4).build()

```


### Прототип (Клон, Prototype)

Прототип — позволяет копировать объекты, не вдаваясь в подробности их реализации.

```js

const wheelsFactory = (type) => {
  const wheels = (country) => ({
    country
  });

  const wheelsMap = {
    simply: wheels("china"),
    medium: wheels("germany")
  };

  return wheelsMap[type];
};

function CarPrototype(type, price, color, doors) {
  this.type = type;
  this.price = price;
  this.color = color;
  this.doors = doors;
  this.wheels = wheelsFactory(price > 1000 ? "simply" : "medium");

  this.print = () => {
    return this;
  };

  this.clone = () => {
    const clone = Object.create(this);
    clone.wheels = {
      ...this.wheels,
      prototype: {
        ...this
      }
    };
    return clone;
  };
}

const car1 = new CarPrototype("sport", 10000, "red", 2);

console.log(car1.clone());

```

### Одиночка (Singleton)

Одиночка гарантирует, что у класса есть только один экземпляр, и предоставляет к нему глобальную точку доступа.

```js

let instance = null;

class SingletonCounter {
  constructor() {
    if (!instance) {
      this.counter = 0;
      instance = this;
    }

    return instance;
  }

  increment() {
    this.counter++;
  }

  decrement() {
    this.counter++;
  }
}

const counter1 = new SingletonCounter();
counter1.decrement();
counter1.decrement();
counter1.decrement();

console.log(counter1.counter);

const counter2 = new SingletonCounter();

console.log(counter2.counter);

```


## Структурные паттерны

### Адаптер (Adapter)

Адаптер — позволяет подружить несовместимые объекты.

```js

class EngineNode {
  run(payload) {
    console.log(`[NODE][RUN] ---> ${payload}`);
  }
}

class EngineDeno {
  constructor() {
    this.code = "";
  }

  transpile(payload) {
    this.code = payload;
  }

  run() {
    console.log(`[DENO][RUN] ---> ${this.code}`);
  }
}

class EngineDenoAdapter {
  constructor(EngineDeno) {
    this.deno = new EngineDeno();
  }

  run(payload) {
    this.deno.transpile(payload);
    this.deno.run();
  }
}

const node = new EngineNode().run("hello world");

const deno = new EngineDenoAdapter(EngineDeno).run("hello world");

```

### Мост (Bridge)

Мост — разделяет бизнес-логику или большой класс на несколько отдельных иерархий, которые потом можно развивать отдельно друг от друга.

### Компоновщик (Composite)

Компоновщик — позволяет сгруппировать множество объектов в древовидную структуру, а затем работать с ней так, как будто это единичный объект.

### Декоратор (Decorator)

Декоратор позволяет динамически добавлять объектам новую функциональность, оборачивая их в полезные «обёртки».

```js
class WebComponet {
  static render() {
    return "<h1>Hello world</h1>";
  }
}

// Class decorator

class Logger {
  static print(component) {
    console.log("[CLASS][LOGGER] render");

    return component;
  }
}

// Function decorator

const logger = (component) => {
  console.log("[FUNCTION][LOGGER] render");

  return component;
};

Logger.print(WebComponet);

logger(WebComponet);

```

### Фасад (Facade)

Фасад предоставляет простой интерфейс к сложной системе классов, библиотеке или фреймворку. Фасад может иметь урезанный интерфейс, не имеющий 100% функциональности, которой можно достичь, используя сложную подсистему напрямую. Но он предоставляет именно те фичи, которые нужны клиенту, и скрывает все остальные.

### Легковес

### Заместитель

## Поведенческие паттерны 

### Цепочка обязанностей

### Команда

### Итератор

### Посредник

### Снимок

### Наблюдатель

### Состояние

### Стратегия

### Шаблонный метод

### Посетитель (Visitor)

Посетитель — позволяет добавлять в программу новые операции, не изменяя классы объектов, над которыми эти операции могут выполняться.