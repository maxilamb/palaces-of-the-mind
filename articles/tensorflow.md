# Tensorflow JS

https://js.tensorflow.org/api/latest


## Основные слои

* Dense - обычный плотно связанный слой NN.
* Dropout - применяет отсев к входным данным.
* Flatten - выравнивает вход. Не влияет на размер партии.
* Permute - изменяет размеры входных данных в соответствии с заданным шаблоном. Полезно, для соединения RNNS и convnets вместе.
* RepeatVector - повторяет ввод n раз в новом измерении.
* Reshape - Изменяет форму входных данных до определенной формы.



Векторные данные — двумерные тензоры формы [числоПримеров, признаки].  
* Данные в виде временных рядов (последовательностей) — трехмерные тензоры
формы [числоПримеров, интервалы времени, признаки].  
* Изображения — 4-мерные тензоры формы [числоПримеров, высота, ширина, каналы].  
* Видеоданные — 5-мерные тензоры формы [числоПримеров, кадр, высота, ширина,
каналы].  


`Layers` - 

* conv2d -   
* maxPooling2d - 

`Optimizer` - алгоритм обновления сетью своих весов на основе данных и функции потерь.

* Adadelta -Implements the Adadelta algorithm.
* Adagrad - Implements the Adagrad algorithm.
* Adam - Implements the Adam algorithm.
* Adamax - Implements the Adamax algorithm.
* Ftrl - Implements the FTRL algorithm.
* Nadam - Implements the NAdam algorithm.
* Optimizer - Base class for Keras optimizers.
* RMSprop - Implements the RMSprop algorithm.
* SGD - Stochastic Gradient Descent Optimizer.

`Loss function` - метрика погрешности модели. Она определяет как модель предсказывает на основе данных и объекта правильного ответа.

* meanAbsoluteError - вычесляется по формуле `meanAbsoluteError = average(absolute(modelOutput - targets))`  
* meanSquaredError -  Среднее арифметическое квадратов разностей между предсказанными и реальными значениями Модели  
* categoricalCrossentropy - 

`Activation function`

* sigmoid
* relu
* softmax


### Model

##### Shapes and Units

inputShape: [1] because we have 1 input (x = horsepower).  

units: 1 defines the size of the weight matrix: 1 weight for each input (x value).  

`fit()` - обучение модели на основе данных.  
`evaluate()` - оценка модели на основе данных (вычисляет функцию потерь).  
`predict()` - предсказание на основе данных.  
`summary()` - описание модели.  
`save()` - сохранение модели.  
`load()` - загрузка модели.

### tf

`mean()` - вычисление среднего значения.  
`sub()` - вычитание двух тензоров.
`square()` - возведение в квадрат.  
`sqrt()` - возведение в квадратный корень.  
`div()` - деление двух тензоров.  

### Training

```js

async function trainModel(model, inputs, labels, surface) {
  const batchSize = 25;
  const epochs = 100;
  const callbacks = tfvis.show.fitCallbacks(surface, ['loss'], {callbacks:['onEpochEnd']});
  
  return await model.fit(inputs, labels,
    {batchSize, epochs, shuffle:true, callbacks:callbacks}
  );
}
```

`epochs` defines how many iterations (loops) the model will do.  

`model.fit` is the function that runs the loops.  

`callbacks` defines the callback function to call when the model wants to redraw the graphics.  


### examples

`fit()`

```js
await model.fit(tensors.trainFeatures, tensors.trainTarget, {
    batchSize: BATCH_SIZE, // количество объектов в батче
    epochs: NUM_EPOCHS, // количество эпох для обучения
    validationSplit: 0.2, // процент данных для валидации из обучающей выборки для предотвращения переобучения
});

```
