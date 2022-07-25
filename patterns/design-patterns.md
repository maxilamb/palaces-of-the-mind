# Паттерны проектирования

Паттерн проектирования — это часто встречающееся решение определённой проблемы при проектировании архитектуры программ.

* **Порождающие** паттерны беспокоятся о гибком создании объектов без внесения в программу лишних зависимостей.
* **Структурные** паттерны показывают различные способы построения связей между объектами.
* **Поведенческие** паттерны заботятся об эффективной коммуникации между объектами.

## Пораждающий паттерн

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