# JavaScript Best Practices


### 1. Объявление переменных.
Используйте `const` для объявления переменных; избегайте `var`. eslint: `prefer-const`, `no-const-assign`.
> Это гарантирует, что вы не сможете переопределять значения, т.к. это может привести к ошибкам и к усложнению понимания кода.

**bad practice**
  var a = 1;
  var b = 2;

**good practice**
  const a = 1;
  const b = 2;


### 2. Порядок объявления переменных.

Это считается хорошей практикой написания кода и влечёт за собой:

+ Более "чистый" код на выходе;
+ Единое место для поиска локальных переменных;
+ Возможность избежать объявления нежелательных глобальных переменных;
+ Уменьшает вероятность нежелательных повторных объявлений переменных.


  // Объявление переменных в начале
  let firstName, lastName, yearOfBirth, currentYear, age;
  
  // Использование в дальнейшем
  firstName = "Sam";
  lastName = "Smith";

  yearOfBirth = 1996;
  currentYear = 2021;

  age = currentYear - yearOfBirth;


### 3. Для создания объекта используйте литеральную нотацию.

  **bad practice**
  const item = new Object();

  **good practice**
  const item = {};


### 4. Операторы сравнения.
Следует использовать строгое сравнение (=== или !==) вместо нестрогого (== или !=). Это позволит избавиться от неявного преобразования типа данных.

  **bad practice**
  if (answer == 4) { console.log(true); } if (attempts != 0) { console.log('Ты пытался') };

  **good practice**
  if (answer === 4) { console.log(true); } if (attempts !== 0) { console.log('Ты пытался') };


### 5. Названия объектов языка должны отражать их значение/функции.
Названия переменных должны отражать тип значения и контекст, в котором они будут использоваться.
Названия функций должны отражать их назначение или получаемый результат.
  
  **bad practice**
  const a = 10;
  const anotherString = '...';
  const human = true;
  const date = () => {
    const currentTime = new Date();
    return currentTime;
  };

  **good practice**
  const length = 10;
  const thirdString = '...';
  const isHuman = true;
  const getDate = () => {
    const currentTime = new Date();
    return currentTime;
  };


### 6. Точка с запятой.
Каждое предложение должно отделяться точкой с запятой. Полагаться на автоматическую вставку точек с запятыми запрещается.

  **bad practice**
  let age = prompt("Сколько Вам лет?", 18) 
  let welcome if (age < 18) {
       welcome = function() { 
           alert("Привет!") 
           }
 } else { 
     welcome = function() { 
         alert("Здравствуйте!") 
         }
         } welcome()

  **good practice**
   let age = prompt("Сколько Вам лет?", 18);
   let welcome if (age < 18) {
       welcome = function() { 
           alert("Привет!") 
           };
 }; else { 
     welcome = function() { 
         alert("Здравствуйте!") 
         };
         }; welcome()

### 7. Кавычки.
Рекомендуется использовать одиночные кавычки (''), либо обратные (``) при использовании шаблонных строк.

 **bad practice**
  const username = "John";

  **good practice**  
  const username = 'Mark'; const greeting = Oh hi ${username}!


### 8. Методы.
Не вызывайте напрямую методы `Object.prototype`, такие как `hasOwnProperty`, `propertyIsEnumerable` и `isPrototypeOf`. 
> Эти методы могут быть переопределены в свойствах объекта, который мы проверяем `{ hasOwnProperty: false }`, или этот объект может быть `null` (`Object.create(null)`).

**bad practice**
  console.log(object.hasOwnProperty(key));

**good practice**
  console.log(Object.prototype.hasOwnProperty.call(object, key));

  **or**
  const has = Object.prototype.hasOwnProperty; // Кэшируем запрос в рамках модуля.
  console.log(has.call(object, key));


### 9. Оптимизировать циклы.
Циклы могут работать весьма быстро, если описывать их правильно.
Одна из самых распространённых ошибок - вычисление длинны массива на каждой итерации цикла:

**bad practice**
const groups = ['BTS', 'ATEEZ', 'Mamamoo', 'Red Velvet'];
for (let i = 0; i < groups.length; i++){
  doSomeThingWith(groups[i]);
};

**good practice**
const groups = ['BTS', 'ATEEZ', 'Mamamoo', 'Red Velvet'];
let j = groups.length;
for (let i = 0; i < j; i++){
  doSomeThingWith(groups[i]);
};


### 10. Комментировать столько, сколько необходимо.
Комментарии - это ваши сообщения другим разработчикам (либо себе в будущем).
Хороший код, возможно, и должен комментировать себя сам, но не факт, что каждый разработчик сможеть быстро и правильно разобрать отдельные его части в данном контексте программы.

Комментарии не исполняются интерпретатором JavaScript. Однострочные комментарии начинаются с двойного слэша //. За ним обязательно должен идти пробел; 
Многострочные комментарии располагаются между /* и */. За символом начала комментария обязательно должен идти пробел. Символ конца комментария располагается на новой строке.