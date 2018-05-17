# Стиль написання JavaScript від компанії Airbnb

*Найбільш обгрунтований підхід до JavaScript*

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Інші керівництва по стилю
 - [ES5 (Deprecated)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
 - [React](react/)
 - [CSS-in-JavaScript](css-in-javascript/)
 - [CSS & Sass](https://github.com/airbnb/css)
 - [Ruby](https://github.com/airbnb/ruby)

## Зміст

  1. [Типи](#Типи)
  1. [Посилання](#Посилання)
  1. [Об'єкти](#Об'єкти)
  1. [Масиви](#Масиви)
  1. [Деструктурування](#Деструктурування)
  1. [Рядки](#Рядки)
  1. [Функції](#Функції)
  1. [Arrow-функції](#Arrow-функції)
  1. [Класи та Конструктори](#Класи-та-Конструктори)
  1. [Модулі](#Модулі)
  1. [Ітератори та Генератори](#Ітератори-та-генератори)
  1. [Властивості](#Властивості)
  1. [Змінні](#Змінні)
  1. [Підняття (Hoisting)](#Підняття-(Hoisting))
  1. [Оператори порівняння і рівності](#Оператори-порівняння-та-рівності)
  1. [Блоки](#Блоки)
  1. [Коментарі](#Коментарі)
  1. [Пробіли](#Пробіли)
  1. [Коми](#Коми)
  1. [Крапка з комою](#Крапка-з-комою)
  1. [Приведення типів та Примушення (Coercion)](#Приведення-типів-та-Примушення)
  1. [Угоди про іменування](#Угоди-про-іменування)
  1. [Аксессори](#Аксессори)
  1. [Події](#Події)
  1. [jQuery](#jquery)
  1. [ECMAScript 5 сумісність](#ecmascript-5-сумісність)
  1. [ECMAScript 6+ (ES 2015+) стилі](#ecmascript-6-es-2015-стилі)
  1. [Тестування](#Тестування)
  1. [Продуктивність](#Продуктивність)
  1. [Ресурси](#Ресурси)
  1. [В реальному Світі](#В-реальному-світі)
  1. [Переклад](#Переклад)
  1. [Керівництво зі стилю написання JavaScript](#the-javascript-style-guide-guide)
  1. [Поговоріть з нами про JavaScript](#chat-with-us-about-javascript)
  1. [Автори](#contributors)
  1. [License](#license)

## Типи

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **Примітиви**: Коли ви отримуєте доступ до примітиву, ви працюєте напряму з його значенням.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **Складні типи**: Коли ви отримуєте доступ до складного типу, ви працюєте з посиланням на його значення.

    + `object`
    + `array`
    + `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ вверх](#Зміст)**

## Посилання

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) Використовуйте `const` для всіх посилань; уникайте використання `var`. eslint: [`prefer-const`](http://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign.html)

    > Чому? Це убезпечить вас від переприсвоєння значення для вашого посилання, що може призвести до багів та складності розуміння коду.

    ```javascript
    // погано
    var a = 1;
    var b = 2;

    // добре
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) Якщо ви пеприсвоюєте посилання -  використовуйте `let` замість `var`. eslint: [`no-var`](http://eslint.org/docs/rules/no-var.html) jscs: [`disallowVar`](http://jscs.info/rule/disallowVar)

    > Чому? `let` має блочну область видимості, на відміну від `var`, область видимості котрого обмежена функцією.

    ```javascript
    // погано
    var count = 1;
    if (true) {
      count += 1;
    }

    // добре, використовуйте let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) Зауважте, що і `let` і `const` мають блочну область видимості.

    ```javascript
    // const та let існують лише в межах блоку, в якому вони були визначені.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ вверх](#Зміст)**

## Об'єкти

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) Використовуйте літерали (фігурні скобки) для створення нового об'єкта. Не використовуйте для створення нового об'єкта конструктор `new Object`. eslint: [`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // погано
    const item = new Object();

    // добре
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) Використовуйте вираховані імена властивостей, при створенні об'єктів з динамічними іменами властивостей.

    > Чому? Вони дозволяють визначати всі властивості об'єкта в одному місці.

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // погано
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // добре
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) Використовуйте скорочення для метода об'єкта. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

    ```javascript
    // погано
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // добре
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) Використовуйте скорочення значення властивості. eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

    > Чому? Так менше писати і більш зрозуміло.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // погано
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // добре
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) Групуйте ваші скорочені властивості на початку оголошення вашого об'єкту.

    > Чому? Так легше сказати які властивості використовують скорочення.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // погано
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // добре
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) Беріть в лапки лише ті властивості, які є неприпустимими ідентифікаторами. eslint: [`quote-props`](http://eslint.org/docs/rules/quote-props.html) jscs: [`disallowQuotedKeysInObjects`](http://jscs.info/rule/disallowQuotedKeysInObjects)

  > Чому? В загальному, ми вважаємо, що так суб'єктивно легше читати. Це покращує підсвітку синтаксису, а також більш легко оптимізується багатьма JS двигунами.

  ```javascript
  // погано
  const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
  };

  // добре
  const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
  };
  ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) Не використовуйте напряму методи `Object.prototype`, такі як `hasOwnProperty`, `propertyIsEnumerable`, і `isPrototypeOf`.
  > Чому? Ці методи можуть бути переоприділені на поточному об'єкті, наприклад: `{ hasOwnProperty: false }`, або ж поточний об'єкт може не мати прототипа (`Object.create(null)`).

  ```javascript
  // погано
  console.log(object.hasOwnProperty(key));

  // добре
  console.log(Object.prototype.hasOwnProperty.call(object, key));

  // найкраще
  const has = Object.prototype.hasOwnProperty; // закешовуємо результати пошуку у скоупі модуля.
  /* або */
  import has from 'has';
  …
  console.log(has.call(object, key));
  ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) Віддавайте перевагу `spread` оператору над [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) для дрібного копіювання об'єктів. Використовуйте `rest` оператор для отримання нового об'єкта з певними відсутніми властивостями.

  ```javascript
  // дуже погано
  const original = { a: 1, b: 2 };
  const copy = Object.assign(original, { c: 3 }); // це мутує `original` ಠ_ಠ
  delete copy.a; // це також

  // погано
  const original = { a: 1, b: 2 };
  const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

  // добре
  const original = { a: 1, b: 2 };
  const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

  const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
  ```

**[⬆ вверх](#Зміст)**

## Масиви

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) Використовуйте синтаксис літерала для створення масиву. eslint: [`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // погано
    const items = new Array();

    // добре
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) Використовуйте [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) замість прямого запису елементів у масив.

    ```javascript
    const someStack = [];

    // погано
    someStack[someStack.length] = 'abracadabra';

    // добре
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) Використовуйте `...`( `spreads` ) оператор масива для копіювання масивів.

    ```javascript
    // погано
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // добре
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a><a name="4.4"></a>
  - [4.4](#arrays--from) Для конвертації масивоподібних об'єктів в масив, використовуйте [Array.from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

    ```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.5](#arrays--callback-return) Використовуйте оператор `return` у функціях зворотнього виклику методу масива. Це нормально не робити повернення, якщо тіло функції складається з одного визначення згідно з [8.2](#8.2). eslint: [`array-callback-return`](http://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // добре
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // добре
    [1, 2, 3].map(x => x + 1);

    // погано
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
    });

    // добре
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
      return flatten;
    });

    // погано
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // добре
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

**[⬆ вверх](#Зміст)**

## Деструктурування

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) Використовуйте деструктурування об'єкта, коли отримуєте доступ і використовуєте декілька властивостей об'єкта. jscs: [`requireObjectDestructuring`](http://jscs.info/rule/requireObjectDestructuring)

    > Чому? Деструктурування вберігає вас від створення тимчасових посиланнь на ті властивості.

    ```javascript
    // погано
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // добре
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // найкраще
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) Використовуйте деструктурування масивів. jscs: [`requireArrayDestructuring`](http://jscs.info/rule/requireArrayDestructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // погано
    const first = arr[0];
    const second = arr[1];

    // добре
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) Використовуйте деструктурування об'єкта, а не масива, для декількох повертаємих значеннь . jscs: [`disallowArrayDestructuringReturn`](http://jscs.info/rule/disallowArrayDestructuringReturn)

    > Чому? Ви зможете з часом додати нові властивості або змінити послідовність речей не порушуючи розташування викликів.

    ```javascript
    // погано
    function processInput(input) {
      // то відбувається чудо
      return [left, right, top, bottom];
    }

    // Виклик повинен подумати про послідовність повертаємих даних
    const [left, __, top] = processInput(input);

    // добре
    function processInput(input) {
      // то відбувається чудо
      return { left, right, top, bottom };
    }

    // виклик обирає лише необхідні йому данні
    const { left, top } = processInput(input);
    ```


**[⬆ вверх](#Зміст)**

## Рядки

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) Використовуйте одинарні лапки `''` для рядків. eslint: [`quotes`](http://eslint.org/docs/rules/quotes.html) jscs: [`validateQuoteMarks`](http://jscs.info/rule/validateQuoteMarks)

    ```javascript
    // погано
    const name = "Capt. Janeway";

    // погано - літеральні шаблони мають містити інтерполяцію чи нові рядки
    const name = `Capt. Janeway`;

    // добре
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) Рядки, які подовжують лінію більше ніж на 100 символів не повинні записуватись у кілька рядків за допомогою конкатенації

    > Чому? З розбитими таким чином рядками болючіше працювати і вони роблять код важко читаємим.

    ```javascript
    // погано
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // погано
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // добре
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) Коли програмно будуєте рядки, використовуйте рядкові шаблони замість конкатенації. eslint: [`prefer-template`](http://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](http://eslint.org/docs/rules/template-curly-spacing) jscs: [`requireTemplateStrings`](http://jscs.info/rule/requireTemplateStrings)

    > Чому? Рядкові шаблони дають читабельність, короткий синтаксис з переносом нових ліній та функціями інтерполяції рядка.

    ```javascript
    // погано
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // погано
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // погано
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // добре
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) Ніколи не використовуйте `eval()` на рядку, це відкриває дуже багато вразливостей.

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) Не зловживайте символами екранування у рядках. eslint: [`no-useless-escape`](http://eslint.org/docs/rules/no-useless-escape)

    > Чому? Зворотні слеші ('\') шкодять читаємості, тому вони мають використовуватись лише там де дійсно необхідно.

    ```javascript
    // погано
    const foo = '\'this\' \i\s \"quoted\"';

    // добре
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ вверх](#Зміст)**


## Функції

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) Використовуйте іменовані функціональні вирази замість функціональних оголошень. eslint: [`func-style`](http://eslint.org/docs/rules/func-style) jscs: [`disallowFunctionDeclarations`](http://jscs.info/rule/disallowFunctionDeclarations)

    > Чому? Функціональні оголошення хойстяться (вспливають уверх), це означає, що дуже легко послатися на функцію до того, як вона оголошена у файлі. Це шкодить читаємості та підтримуємості. Якщо вам здається, що визначення функції досить велике чи воно ускладнює розуміння іншої частини файлу, то, можливо, прийшов час, щоб виокремити це в окремий модуль! Не забувайте іменувати вирази - анонімні функції можуть ускладнити локалізацію проблеми у стеку викликів. ([Discussion](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // погано
    const foo = function () {
    };

    // погано
    function foo() {
    }

    // добре
    const foo = function bar() {
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) Огортайте негайно виконувані функціональні вирази (НВФВ) у дужки. eslint: [`wrap-iife`](http://eslint.org/docs/rules/wrap-iife.html) jscs: [`requireParenthesesAroundIIFE`](http://jscs.info/rule/requireParenthesesAroundIIFE)

    > Чому? Негайно виконуваний функціональний вираз являє собою єдиний блок - огортання обох, і його і його виклику чітко це показує. Варто зауважити, що у світі де модулі повсюди, вам майже ніколи не потрібен НВФВ.

    ```javascript
    // Негайно виконуваний функціональний вираз (НВФВ)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) Ніколи не оголошуйте функцію у нефункціональному блоці(if, while, etc). Натомість, призначте функцію змінній. Браузери дозволять вам це зробити, але всі вони інтерпретують це по-різному, що є поганими новинами. eslint: [`no-loop-func`](http://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **Увага:** ECMA-262 визначає `block` як список визначень. Оголошення функції не є визначенням. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // погано
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // добре
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) Ніколи не називайте параметр як `arguments`. Це матиме пріоритет над `arguments` об'єкта, який надається області видимості кожної функції.

    ```javascript
    // погано
    function nope(name, options, arguments) {
      // ...щось відбувається...
    }

    // добре
    function yup(name, options, args) {
      // ...щось відбувається...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) Ніколи не використовуйте `arguments`, краще натомість використовуйте `rest` синтаксис (`...`). eslint: [`prefer-rest-params`](http://eslint.org/docs/rules/prefer-rest-params)

    > Чому? `...` оператор явно зазначає, що ви хочете щось витягти. Крім того, rest аргументи являються реальним масивом, а не масивоподібністю, як `arguments`.

    ```javascript
    // погано
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // добре
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) Використовуйте синтаксис "параметру за замовчуванням", а не мутуйте аргументи функції.

    ```javascript
    // насправді погано
    function handleThings(opts) {
      // Ні! Ми не повинні мутувати аргументи функції.
      // Двічі погано: якщо `opts` є неправдивим(`falsy` - прим. прекладача), то воно так і буде задано об'єкту. Це, звісно, може бути тим, що
      // вам саме потрібно, але це може призвести до тонких багів.
      opts = opts || {};
      // ...
    }

    // все ще погано
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // добре
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) Уникайте сторонніх ефектів при використанні параметрів за замовчуванням.

    > Чому? Вони збентежують.

    ```javascript
    var b = 1;
    // погано
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) Завжди зазначайте параметри за замовчуванням останніми.

    ```javascript
    // погано
    function handleThings(opts = {}, name) {
      // ...
    }

    // добре
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) Ніколи не використовуйте конструктор функцій для створення нової функції. eslint: [`no-new-func`](http://eslint.org/docs/rules/no-new-func)

    > Чому? Створення функції таким чином обчислює рядок аналогічно eval(), що, в свою чергу, відкриває вразливості.

    ```javascript
    // погано
    var add = new Function('a', 'b', 'return a + b');

    // досі погано
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) Відступи у сигнатурі функції. eslint: [`space-before-function-paren`](http://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks)

    > Чому? Постійність - це добре, і ви не повинні додавати або видаляти пробіл при додаванні або видаленні імені.

    ```javascript
    // погано
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // добре
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) Ніколи не мутуйте параметри. eslint: [`no-param-reassign`](http://eslint.org/docs/rules/no-param-reassign.html)

    > Чому? Маніпулювання об'єктами, які були передані як параметри, може призвести до небажаних побічних ефектів у змінних, у місці звідки відбувся початковий виклик.

    ```javascript
    // погано
    function f1(obj) {
      obj.key = 1;
    };

    // добре
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    };
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) Ніколи не перепризначайте параметри. eslint: [`no-param-reassign`](http://eslint.org/docs/rules/no-param-reassign.html)

    > Чому? Перепризначення параметрів може призвести до неочікуваної поведінки, особливо, при доступі до об'єкту аргументів. Це також може викликати оптимізаційні проблеми, особливо у V8.

    ```javascript
    // погано
    function f1(a) {
      a = 1;
    }

    function f2(a) {
      if (!a) { a = 1; }
    }

    // добре
    function f3(a) {
      const b = a || 1;
    }

    function f4(a = 1) {
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Віддавайте перевагу використанню `...` (оператор `spread`) при виклику функцій зі змінним числом параметрів . eslint: [`prefer-spread`](http://eslint.org/docs/rules/prefer-spread)

    > Чому? Так чистіше, вам не потрібно надавати контекст і ви не можете легко створити `new` за допомогою `apply`.

    ```javascript
    // погано
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // добре
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // погано
    new (Function.prototype.bind.apply(Date, [null, 2016, 08, 05]));

    // добре
    new Date(...[2016, 08, 05]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) Функції з кількома сигнатурами, чи викликами, повинні бути з відступами, так само як і будь-який інший список у кілька рядків у цьому керівництві: з кожним елементом на своєму рядку, з комою у кінці кожного рядка.

    ```javascript
    // погано
    function foo(bar,
                 baz,
                 quux) {
      // тіло функції
    }

    // добре
    function foo(
      bar,
      baz,
      quux,
    ) {
      // тіло функції
    }

    // погано
    console.log(foo,
      bar,
      baz);

    // добре
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ вверх](#Зміст)**

## Arrow-функції

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) Коли вам потрібно використати функціональний вираз (так само якщо потрібно передати анонімну функцію) - використовуйте позначення arrow-функції. eslint: [`prefer-arrow-callback`](http://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](http://eslint.org/docs/rules/arrow-spacing.html) jscs: [`requireArrowFunctions`](http://jscs.info/rule/requireArrowFunctions)

    > Чому? Це створює версію функції, яка виконується у контексті `this`, що вам зазвичай і потрібно, і має коротший синтаксис.

    > Чому ні? Якщо у вас є досить складна функція, ви можете винести складну логіку з неї у її власну оголошену функцію.

    ```javascript
    // погано
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // добре
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) Якщо тіло функцій складається з одного виразу - не застосовуйте фігурні дужки, а одразу використовуйте неявне повернення. Або, лишіть фігурні дужки і використайте оператор `return`. eslint: [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](http://eslint.org/docs/rules/arrow-body-style.html) jscs:  [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam), [`requireShorthandArrowFunctions`](http://jscs.info/rule/requireShorthandArrowFunctions)

    > Чому? Синтаксичний цукор. Це гарно читається, особливо коли кілька функцій формують послідовний ланцюжок.

    ```javascript
    // погано
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // добре
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // добре
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // добре
    [1, 2, 3].map((number, index) => ({
      [index]: number
    }));
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) У випадку, коли вираз розбивається на декілька рядків, огорніть його у дужки для кращої читаємості.

    > Чому? Це чітко показує де функція починається і де закінчується.

    ```js
    // погано
    ['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod

    );

    // добре
    ['get', 'post', 'put'].map(httpMethod => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) Якщо ваша функція приймає єдиний аргумент і ви не використовуєте дужки - не використайте в такому разі і фігурні дужки. В іншому випадку, завжди огортайте аргументи дужками. eslint: [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html) jscs:  [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam)

    > Чому? Менше візуального безладу.

    ```js
    // погано
    [1, 2, 3].map((x) => x * x);

    // добре
    [1, 2, 3].map(x => x * x);

    // добре
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // погано
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // добре
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) Уникайте синтаксису arrow-функції (`=>`) з операторами порівняння (`<=`, `>=`), оскільки це може збити з пантелику. eslint: [`no-confusing-arrow`](http://eslint.org/docs/rules/no-confusing-arrow)

    ```js
    // погано
    const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

    // погано
    const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

    // добре
    const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

    // добре
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height > 256 ? largeSize : smallSize;
    };
    ```

**[⬆ вверх](#Зміст)**


## Класи та Конструктори

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) Завжди використовуйте `class`. Уникайте маніпулювати `prototype` напряму.

    > Чому? `class` синтаксис коротший і його легше зрозуміти.

    ```javascript
    // погано
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };


    // добре
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) Використовуйте `extends` для наслідування.

    > Чому? Це вбудований спосіб, щоб наслідувати функціональність прототипу, не порушуючи `instanceof`.

    ```javascript
    // погано
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this._queue[0];
    }

    // добре
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) Методи можуть повертати `this`, щоб допомогти методу з побудовою ланцюжка.

    ```javascript
    // погано
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // добре
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) Це нормально писати власний toString() метод, просто переконайтесь, що він працює вдало і без побічних ефектів.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) Класи мають конструктор за замовчуванням, якщо не вказано іншого. Порожній конструктор функції або конструктор, який просто посилається на батьківський клас не є необхідними. eslint: [`no-useless-constructor`](http://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // погано
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // погано
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // добре
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) Уникайте дублювання членів класу. eslint: [`no-dupe-class-members`](http://eslint.org/docs/rules/no-dupe-class-members)

    > Чому? Продубльовані оголошення членів класу будуть нишком віддавати перевагу останньому, тому наявність дублікатів майже напевно - помилка.

    ```javascript
    // погано
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // добре
    class Foo {
      bar() { return 1; }
    }

    // добре
    class Foo {
      bar() { return 2; }
    }
    ```


**[⬆ вверх](#Зміст)**


## Модулі

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) Завжди віддавайте перевагу використанню (`import`/`export`) модуля, а не нестандартній модульній системі. Ви завжди можете сконвертувати(transpile) до вашої улюбленої модульної системи.

    > Чому? Модулі - це майбутнє, тож давайте використовувати майбутнє вже зараз.

    ```javascript
    // погано
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // нормально
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // найкраще
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) Ніколи не вживайте непередбачувані імпорти.

    > Чому? Це гарантує, що у вас по замовчуванню експортується лише один модуль.

    ```javascript
    // погано
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // добре
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) І не експортуйте напряму з імпорту.

    > Чому? Не дивлячись на те, що одна строка це досить коротко, мати один чіткий шлях для імпорта і один чіткий шлях для експорта робить речі більш зрозумілими.

    ```javascript
    // погано
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // добре
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) Імпортуйте з одного місця лише раз.
 eslint: [`no-duplicate-imports`](http://eslint.org/docs/rules/no-duplicate-imports)
    > Чому? Коли є кілька рядків, які імпортують з одного шляху - це ускладнює підтримку коду.

    ```javascript
    // погано
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // добре
    import foo, { named1, named2 } from 'foo';

    // добре
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) Не експортуйте мутабельні прив'язки.
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    > Чому? Взагалі, мутацій потрібно уникати, особливо при експорті мутабельних прив'язок. Хоча цей прийом(мутація) може бути потрібним в деяких особливих ситуаціях, але в загальному потрібно експортувати лише постійні посилання.

    ```javascript
    // погано
    let foo = 3;
    export { foo }

    // добре
    const foo = 3;
    export { foo }
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) У модулі з єдиним експортом віддавайте превагу експорту за замовчуванням (`default`), а не іменованому експорту.
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)

    ```javascript
    // погано
    export function foo() {}

    // добре
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) Зазначайте всі `import` визначення над не імпортами.
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
    > Чому? Оскільки `import`и вспливають вгору, то тримати їх зверху убезпечує від неочікуваної поведінки.

    ```javascript
    // погано
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // добре
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) Імпорти у кілька рядків мають мати такі самі відступи як і масиви чи об'єктні літерали.

    > Чому? Фігурні дужки дотримуються тих самих правил, як і кожен блок з фігурними дужками у цьому керівництві. Те саме стосується і ком у кінці кожного рядка в середині блоку.

    ```javascript
    // погано
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // добре
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) Забороняти `Webpack loader` синтаксис у оголошенні модульного імпорту.
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)
    > Чому? TODO: COMPLETE Since using Webpack syntax in the imports couples the code to a module bundler. Prefer using the loader syntax in `webpack.config.js`.

    ```javascript
    // погано
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // добре
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

**[⬆ вверх](#Зміст)**

## Ітератори та генератори

  <a name="iterators--nope"></a><a name="11.1"></a>
  - [11.1](#iterators--nope) Не використовуйте ітератори. Віддавайте перевагу функціям вищого порядку замість циклів, таких як `for-in` чи `for-of`. eslint: [`no-iterator`](http://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](http://eslint.org/docs/rules/no-restricted-syntax)

    > Чому? Це примушує дотримуватись нашого правила не мутувати дані. Легше працювати з чистими функціями які повертають значення, а не побічні ефекти.

    > Використовуйте `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... щоб перебирати масиви, і `Object.keys()` / `Object.values()` / `Object.entries()` для створення масивів, щоб мати змогу далі їх перебирати.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // погано
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // добре
    let sum = 0;
    numbers.forEach(num => sum += num);
    sum === 15;

    // найкраще (використовуйте функціональну силу)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // погано
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // добре
    const increasedByOne = [];
    numbers.forEach(num => increasedByOne.push(num + 1));

    // найкраще (притримуйтесь функціонального стилю)
    const increasedByOne = numbers.map(num => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) Поки що не використовуйте генератори.

    > Чому? Вони не досить добре перетворюються в ES5.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) Якщо вам потрібно використати генератори, або якщо ви вирішили не скористатись нашою порадою [our advice](#generators--nope), переконайтесь, що сигнатура функції має правильні відступи. eslint: [`generator-star-spacing`](http://eslint.org/docs/rules/generator-star-spacing)

    > Чому? `function` і `*` є частиною одного концептуального ключового слова - `*` це не модифікатор `function`, `function*` - це унікальна конструкція, відмінна від `function`.

    ```js
    // погано
    function * foo() {
    }

    const bar = function * () {
    }

    const baz = function *() {
    }

    const quux = function*() {
    }

    function*foo() {
    }

    function *foo() {
    }

    // дуже погано
    function
    *
    foo() {
    }

    const wat = function
    *
    () {
    }

    // добре
    function* foo() {
    }

    const foo = function* () {
    }
    ```

**[⬆ вверх](#Зміст)**


## Властивості

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) Використовуйте точкову нотацію при доступі до властивостей. eslint: [`dot-notation`](http://eslint.org/docs/rules/dot-notation.html) jscs: [`requireDotNotation`](http://jscs.info/rule/requireDotNotation)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // погано
    const isJedi = luke['jedi'];

    // добре
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) Використовуйте квадратні дужки `[]` при доступі до властивостей через змінні.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

**[⬆ вверх](#Зміст)**


## Змінні

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) Завжди використовуйте `const` для оголошення змінних. Недотримання цієї вимоги призведе до глобальних змінних. Ми хочемо уникнути забруднення глобального простору імен. Капітан Планета застерігає нас від цього. eslint: [`no-undef`](http://eslint.org/docs/rules/no-undef) [`prefer-const`](http://eslint.org/docs/rules/prefer-const)

    ```javascript
    // погано
    superPower = new SuperPower();

    // добре
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) Використовуйте по одному `const` для кожної змінної. eslint: [`one-var`](http://eslint.org/docs/rules/one-var.html) jscs: [`disallowMultipleVarDecl`](http://jscs.info/rule/disallowMultipleVarDecl)

    > Чому? Так легше оголошувати змінні таким чином, що вам не потрібно буде хвилюватись, що ви випадково переплутаєте в кінці рядка `;` з `,`. Ви також можете пройти через кожне оголошення змінної за допомогою дебагера, замість того, щоб перестрибнути через всі оголошення змінних одразу.

    ```javascript
    // погано
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // погано
    // (порівняйте з верхнім і спробуйте знайти помилку)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // добре
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) Спочатку групуйте всі ваші `const`, а потім вже групуйте всі `let`s.

    > Чому? Це дуже зручно у випадку, коли в подальшому вам знадобиться оголосити зміну в залежності від вже оголошених змінних.

    ```javascript
    // погано
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // погано
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // добре
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) Призначайте змінні де вам потрібно, але розміщуйте їх лише у потрібних місцях.

    > Чому? `let` і `const` обмежуються блочною зоною видимості, а не функціональною.

    ```javascript
    // погано - непотрібний виклик функції
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // добре
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```
  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) Не поєднуйте в ланцюжки присвоєння змінних.

    > Чому? Поєднання змінних у ланцюжки створює неявні глобальні змінні.

    ```javascript
    // погано
    (function example() {
      // JavaScript інтерпретує це як
      // let a = ( b = ( c = 1 ) );
      // Ключове слово let застосовується до змінної a; змінні b та c стають
      // глобальними змінними.
      let a = b = c = 1;
    }());

    console.log(a); // undefined
    console.log(b); // 1
    console.log(c); // 1

    // добре
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // undefined
    console.log(b); // undefined
    console.log(c); // undefined

    // Те ж саме стосується і `const`
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) Уникайте використання унарних збільшеннь та зменшеннь (++, --). eslint [`no-plusplus`](http://eslint.org/docs/rules/no-plusplus)

    > Чому? Згідно з документацією **eslint**, унарні збільшення або зменшення спричиняють автоматичну вставку крапки й коми, що, в свою чергу, може призвести до непомітних помилок при збільшенні або зменшенні значень у рамках програми. Також, більш виразно застосовувати для збільшеннь або зменшень такі вирази як `num += 1` замість `num++` або `num ++`. Заборона унарних збільшеннь або зменшеннь також захищає вас від випадкових попередніх збільшеннь/зменшень, які також можуть призвести до непередбачуваної поведінки у ваших програмах.

    ```javascript
      // погано

      let array = [1, 2, 3];
      let num = 1;
      num++;
      --num;

      let sum = 0;
      let truthyCount = 0;
      for(let i = 0; i < array.length; i++){
        let value = array[i];
        sum += value;
        if (value) {
          truthyCount++;
        }
      }

      // добре

      let array = [1, 2, 3];
      let num = 1;
      num += 1;
      num -= 1;

      const sum = array.reduce((a, b) => a + b, 0);
      const truthyCount = array.filter(Boolean).length;
    ```

**[⬆ вверх](#Зміст)**


## Підняття (Hoisting)

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) Оголошені змінні, за допомогою ключового слова `var`, піднімаються вгору обсласті видимості функції, в той час як привласнені їм значення - ні. Змінні, оголошені за допомогою `const` та `let` отримали нову концепцію - [Тимчасові Мертві Зони (ТМЗ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let). Важливо знати, чому використовувати [typeof тепер небезпечно](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // ми знаємо, що це не спрацює (припустимо, що
    // не існує глобальної змінної notDefined)
    function example() {
      console.log(notDefined); // => видасть ReferenceError
    }

    // створення змінної після того,
    // як на неї зіслались спрацює завдяки підйому змінної
    // Зауважте: присвоєне змінній значення `true` не підніметься вгору.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // інтерпретатор піднімає проголошення змінної
    // вверх області видимості,
    // що означає, що наш приклад може бути записаним як:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // використовуючи const та let
    function example() {
      console.log(declaredButNotAssigned); // => видасть ReferenceError
      console.log(typeof declaredButNotAssigned); // => видасть ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) Анонімні функціональні вирази піднімають ім'я змінної, але не функціональне присвоєння.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expresions) Іменовані функціональні вирази піднімають ім'я змінної, але не ім'я функції чи тіло функції.

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // це також стосується і випадку,
    // коли ім'я функції співпадає з іменем змінної.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      }
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) Функціональне оголошення піднімає ім'я і тіло функції.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - За більш детальною інформацією звертайтесь до [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) автор [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ вверх](#Зміст)**


## Оператори порівняння та рівності

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) Використовуйте `===` та `!==` а не `==` і не `!=`. eslint: [`eqeqeq`](http://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) Умовні оператори, такі як `if` вираховують вираз за допомогою примусового приведення до логічного виразу `ToBoolean` і завжди слідують цим простим правилам:

    + **Objects** оцінюється як **true**
    + **Undefined** оцінюється як **false**
    + **Null** оцінюється як **false**
    + **Booleans** оцінюються як **the value of the boolean**
    + **Numbers** оцінюється як **false**, якщо **+0, -0, or NaN**, в усіх інших випадках як **true**
    + **Strings** оцінюється як **false** якщо рядок порожній `''`, в усіх інших випадках як **true**

    ```javascript
    if ([0] && []) {
      // true
      // масив (навіть якщо він порожній) - це об'єкт, а об'єкт завжди оцінюється як true
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) Використовуйте скорочення для логічних значеннь, але явно зазначайте, коли порівнюєте рядки та числа.

    ```javascript
    // погано
    if (isValid === true) {
      // ...stuff...
    }

    // добре
    if (isValid) {
      // ...stuff...
    }

    // погано
    if (name) {
      // ...stuff...
    }

    // добре
    if (name !== '') {
      // ...stuff...
    }

    // погано
    if (collection.length) {
      // ...stuff...
    }

    // добре
    if (collection.length > 0) {
      // ...stuff...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) Більш детальну інформацію дивіться у статті [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) автора Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) Використовуйте дужки для створення блоків `case` та `default` що містять лексичні декларації (e.g. `let`, `const`, `function`, та `class`).

  > Чому? Лексичні проголошення видимі у всьому `switch` блоці, але вони ініціалізуються лише тоді, коли привласнюються, а це стається лише тоді, коли спрацьювує `case`. Це спричиняє проблеми, коли кілька `case` випадків намагаються визначити одну й ту саму річ.

  eslint rules: [`no-case-declarations`](http://eslint.org/docs/rules/no-case-declarations.html).

    ```javascript
    // погано
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {}
        break;
      default:
        class C {}
    }

    // добре
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {}
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) Тернарні оператори не повинні вкладатись будь яким чином, а мають бути записані в один рядок.

    eslint rules: [`no-nested-ternary`](http://eslint.org/docs/rules/no-nested-ternary.html).

    ```javascript
    // погано
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // краще
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // найкраще
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) Уникайте непотрібних тернарних записів.

    eslint rules: [`no-unneeded-ternary`](http://eslint.org/docs/rules/no-unneeded-ternary.html).

    ```javascript
    // погано
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // добре
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

**[⬆ вверх](#Зміст)**


## Блоки

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) Використовуйте дужки в усіх блоках які записуються у кілька рядків.

    ```javascript
    // погано
    if (test)
      return false;

    // добре
    if (test) return false;

    // добре
    if (test) {
      return false;
    }

    // погано
    function foo() { return false; }

    // добре
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) Якщо ви використовуєте блоки у кілька рядків з `if` та `else`, то ставте `else` на тому самому рядку, що і закриваюча дужка `if` блоку. eslint: [`brace-style`](http://eslint.org/docs/rules/brace-style.html) jscs:  [`disallowNewlineBeforeBlockStatements`](http://jscs.info/rule/disallowNewlineBeforeBlockStatements)

    ```javascript
    // погано
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // добре
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```


**[⬆ вверх](#Зміст)**


## Коментарі

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [17.1](#comments--multiline) Використовуйте `/** ... */` для коментарів у кілька рядків.

    ```javascript
    // погано
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // добре
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [17.2](#comments--singleline) Використовуйте `//` для коментарів в один рядок. Ставте однорядковий коментар на новий рядок одразу над суб'єктом, до якого відноситься цей коментар. Ставте порожній рядок перед коментарем, якщо тільки це не перший рядок блоку.

    ```javascript
    // погано
    const active = true;  // is current tab

    // добре
    // is current tab
    const active = true;

    // погано
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }

    // добре
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }

    // також добре
    function getType() {
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }
    ```

  - [17.3](#comments--spaces) Починайте всі коментарі з пробілу для більше легкого читання. eslint: [`spaced-comment`](http://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // погано
    //is current tab
    const active = true;

    // добре
    // is current tab
    const active = true;

    // погано
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...stuff...

      return element;
    }

    // добре
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [17.4](#comments--actionitems) Починати ваш коментар зі слів `FIXME` чи `TODO` добре, оскільки це допомагає іншим розробникам швидко розуміти, чи ви відзначаєте проблемне місце в коді, яке треба переглянути, чи ви пропонуєте вирішення проблеми, яке має бути запроваджене. Вони відрізняються від звичайних коментарів, оскільки вони вимагають дії. Дія може бути `FIXME: -- потрібно в цьому розібратись і виправити` or `TODO: -- потрібно запровадити`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [17.5](#comments--fixme) Використовуйте `// FIXME:` для описання проблеми.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn't use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [17.6](#comments--todo) Використовуйте `// TODO:` для описання способів вирішення проблеми.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```

**[⬆ вверх](#Зміст)**


## Пробіли

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [18.1](#whitespace--spaces) Використовуйте табуляцію у 2 пробіли. eslint: [`indent`](http://eslint.org/docs/rules/indent.html) jscs: [`validateIndentation`](http://jscs.info/rule/validateIndentation)

    ```javascript
    // погано
    function foo() {
    ∙∙∙∙const name;
    }

    // погано
    function bar() {
    ∙const name;
    }

    // добре
    function baz() {
    ∙∙const name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [18.2](#whitespace--before-blocks) Ставте 1 пробіл перед ведучою фігурною дужкою. eslint: [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks.html) jscs: [`requireSpaceBeforeBlockStatements`](http://jscs.info/rule/requireSpaceBeforeBlockStatements)

    ```javascript
    // погано
    function test(){
      console.log('test');
    }

    // добре
    function test() {
      console.log('test');
    }

    // погано
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // добре
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [18.3](#whitespace--around-keywords) Ставте 1 пробіл перед відкриваючою дужкою у умовах (`if`, `while` і т.д.). Не ставте пробіли між списком аргументів та іменем функції, та між іменем функції та викликами функції і проголошеннями. eslint: [`keyword-spacing`](http://eslint.org/docs/rules/keyword-spacing.html) jscs: [`requireSpaceAfterKeywords`](http://jscs.info/rule/requireSpaceAfterKeywords)

    ```javascript
    // погано
    if(isJedi) {
      fight ();
    }

    // добре
    if (isJedi) {
      fight();
    }

    // погано
    function fight () {
      console.log ('Swooosh!');
    }

    // добре
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [18.4](#whitespace--infix-ops) Розмежовуйте оператори пробілами. eslint: [`space-infix-ops`](http://eslint.org/docs/rules/space-infix-ops.html) jscs: [`requireSpaceBeforeBinaryOperators`](http://jscs.info/rule/requireSpaceBeforeBinaryOperators), [`requireSpaceAfterBinaryOperators`](http://jscs.info/rule/requireSpaceAfterBinaryOperators)

    ```javascript
    // погано
    const x=y+5;

    // добре
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [18.5](#whitespace--newline-at-end) Лишайте символ нового рядку у кінці файлу. eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

    ```javascript
    // погано
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // погано
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // добре
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [18.6](#whitespace--chains) Використовуйте відступи, коли робите ланцюжки методів (більш ніж два методи у ланцюгу). Використовуйте ведучу крапку, яка підкреслює, що на новій лінії відбувається виклик методу, а не нове ствердження. eslint: [`newline-per-chained-call`](http://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](http://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // погано
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // погано
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // добре
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // погано
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // добре
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // добре
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [18.7](#whitespace--after-blocks) Лишайте порожній рядок після блоків і перед наступним ствердженням. jscs: [`requirePaddingNewLinesAfterBlocks`](http://jscs.info/rule/requirePaddingNewLinesAfterBlocks)

    ```javascript
    // погано
    if (foo) {
      return bar;
    }
    return baz;

    // добре
    if (foo) {
      return bar;
    }

    return baz;

    // погано
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // добре
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // погано
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // добре
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [18.8](#whitespace--padded-blocks) Не насичуйте ваші блоки порожніми лініями. eslint: [`padded-blocks`](http://eslint.org/docs/rules/padded-blocks.html) jscs:  [`disallowPaddingNewlinesInBlocks`](http://jscs.info/rule/disallowPaddingNewlinesInBlocks)

    ```javascript
    // погано
    function bar() {

      console.log(foo);

    }

    // також погано
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // добре
    function bar() {
      console.log(foo);
    }

    // добре
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [18.9](#whitespace--in-parens) Не додавайте пробілів в середині дужок. eslint: [`space-in-parens`](http://eslint.org/docs/rules/space-in-parens.html) jscs: [`disallowSpacesInsideParentheses`](http://jscs.info/rule/disallowSpacesInsideParentheses)

    ```javascript
    // погано
    function bar( foo ) {
      return foo;
    }

    // добре
    function bar(foo) {
      return foo;
    }

    // погано
    if ( foo ) {
      console.log(foo);
    }

    // добре
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [18.10](#whitespace--in-brackets) Не ставте зайвих пробілів в середині квадратних дужок. eslint: [`array-bracket-spacing`](http://eslint.org/docs/rules/array-bracket-spacing.html) jscs: [`disallowSpacesInsideArrayBrackets`](http://jscs.info/rule/disallowSpacesInsideArrayBrackets)

    ```javascript
    // погано
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // добре
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [18.11](#whitespace--in-braces) Додавайте пробіли в середині фігурних дужок. eslint: [`object-curly-spacing`](http://eslint.org/docs/rules/object-curly-spacing.html) jscs: [`requireSpacesInsideObjectBrackets`](http://jscs.info/rule/requireSpacesInsideObjectBrackets)

    ```javascript
    // погано
    const foo = {clark: 'kent'};

    // добре
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [18.12](#whitespace--max-len) Уникайте ліній коду, що довші за 100 символів (включаючи пробіли). Примітка: [зазначені тут](#strings--line-length) довгі рядки не підпадають під це правило і не повинні розбиватись. eslint: [`max-len`](http://eslint.org/docs/rules/max-len.html) jscs: [`maximumLineLength`](http://jscs.info/rule/maximumLineLength)

    > Чому? Це забезпечує читаємість та підтримку.

    ```javascript
    // погано
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // погано
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // добре
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // добре
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

**[⬆ вверх](#Зміст)**

## Коми

<a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [19.1](#commas--leading-trailing) Направляючі коми: **Ні.** eslint: [`comma-style`](http://eslint.org/docs/rules/comma-style.html) jscs: [`requireCommaBeforeLineBreak`](http://jscs.info/rule/requireCommaBeforeLineBreak)

    ```javascript
    // погано
    const story = [
        once
      , upon
      , aTime
    ];

    // добре
    const story = [
      once,
      upon,
      aTime,
    ];

    // погано
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // добре
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [19.2](#commas--dangling) Додаткова кома в кінці рядку: **Так.** eslint: [`comma-dangle`](http://eslint.org/docs/rules/comma-dangle.html) jscs: [`requireTrailingComma`](http://jscs.info/rule/requireTrailingComma)

    > Чому? Це веде до чистіших відмінностей у git. Також, транспайелри, такі як Babel, приберуть додаткову кому в кінці рядку з кінцевого коду, що означає, що ви не повинні перейматись через [проблему завершальної коми](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) у старих браузерах.

    ```diff
    // погано - git diff без завершальної коми
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // добре - git diff із завершальною комою
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // погано
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // добре
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // погано
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // добре
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // добре (зауважте, що кома не повинна з'являтись після "rest" елементу)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // погано
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // добре
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // добре (зауважте, що кома не повинна з'являтись після "rest" елементу)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    )
    ```

**[⬆ вверх](#Зміст)**


## Крапка з комою

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [20.1](#20.1) **Так.** eslint: [`semi`](http://eslint.org/docs/rules/semi.html) jscs: [`requireSemicolons`](http://jscs.info/rule/requireSemicolons)

    ```javascript
    // погано
    (function () {
      const name = 'Skywalker'
      return name
    })()

    // добре
    (function () {
      const name = 'Skywalker';
      return name;
    }());

    // добре, але застаріло (захист, щоб функція не перетворювалась на аргумент, коли об'єднуються два файли за допомогою IIFEs(негайно виконуваний функціональний вираз (НВФВ)))
    ;(() => {
      const name = 'Skywalker';
      return name;
    }());
    ```

    [Прочитати більше](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214%237365214).

**[⬆ вверх](#Зміст)**


## Приведення типів та Примушення

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [21.1](#coercion--explicit) Виконуйте примусове приведення типу на початку ствердження.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [21.2](#coercion--strings)  Рядки:

    ```javascript
    // => this.reviewScore = 9;

    // погано
    const totalScore = this.reviewScore + ''; // викликає this.reviewScore.valueOf()

    // погано
    const totalScore = this.reviewScore.toString(); // не гарантовано, що повернеться рядок

    // добре
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [21.3](#coercion--numbers) Цифри: Використовуйте `Number` для приведення типу та `parseInt` завжди з десятичною для синтаксичного аналізу рядків. eslint: [`radix`](http://eslint.org/docs/rules/radix)

    ```javascript
    const inputValue = '4';

    // погано
    const val = new Number(inputValue);

    // погано
    const val = +inputValue;

    // погано
    const val = inputValue >> 0;

    // погано
    const val = parseInt(inputValue);

    // добре
    const val = Number(inputValue);

    // добре
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [21.4](#coercion--comment-deviations) Якщо, з якоїсь причини, ви робите щось дике і `parseInt` являється слабкою ланкою і вам потрібно використати бітову операцію заради [ефективності](https://jsperf.com/coercion-vs-casting/3), залиште коментар, який пояснює навіщо і що ви робите.

    ```javascript
    // добре
    /**
     * parseInt сповільнював код.
     * Застосування бітової операції щодо рядка для примусового приведення до
     * Number робить код набагато швидшим.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [21.5](#coercion--bitwise) **Зауважте:** Будьте обачні при використанні бітових операцій. Цифри представленні як [64-бітні значення](https://es5.github.io/#x4.3.19), але бітові операції завжди повертають 32-bit ціле число ([джерело](https://es5.github.io/#x11.7)). Бітова операція може призвести до непердбачуваної поведінки для цілик значеннь, більших ніж 32-біта. [Обговорення](https://github.com/airbnb/javascript/issues/109). Найбільшим виявленим 32-бітним цілим числом є 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [21.6](#coercion--booleans) Булеві значення:

    ```javascript
    const age = 0;

    // погано
    const hasAge = new Boolean(age);

    // добре
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ вверх](#Зміст)**


## Угоди про іменування

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [22.1](#naming--descriptive) Уникайте імен в одну літеру. Нехай ваші імена будуть описовими. eslint: [`id-length`](http://eslint.org/docs/rules/id-length)

    ```javascript
    // погано
    function q() {
      // ...stuff...
    }

    // добре
    function query() {
      // ..stuff..
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [22.2](#naming--camelCase) Використовуйте `camelCase` коли називаєте об'єкти, функції і екземпляри. eslint: [`camelcase`](http://eslint.org/docs/rules/camelcase.html) jscs: [`requireCamelCaseOrUpperCaseIdentifiers`](http://jscs.info/rule/requireCamelCaseOrUpperCaseIdentifiers)

    ```javascript
    // погано
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // добре
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [22.3](#naming--PascalCase) Використовуйте PascalCase лише коли називаєте конструктори чи класи. eslint: [`new-cap`](http://eslint.org/docs/rules/new-cap.html) jscs: [`requireCapitalizedConstructors`](http://jscs.info/rule/requireCapitalizedConstructors)

    ```javascript
    // погано
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // добре
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [22.4](#naming--leading-underscore) Не використовуйте завершальних чи лідуючих нижніх підкресленнь(underscores). eslint: [`no-underscore-dangle`](http://eslint.org/docs/rules/no-underscore-dangle.html) jscs: [`disallowDanglingUnderscores`](http://jscs.info/rule/disallowDanglingUnderscores)

    > Чому? В JavaScript немає поняття приватності властивостей чи методів. Хоча, лідуюче нижнє підкреслення і прийнято використовувати для позначення "приватності", насправді, ці властивості всі публічні, і тому являються частиною вашого публічного API. Такий підхід може ввести розробниців в оману, що зміна не буде критичною, чи що не потрібні тести. tl;dr: якщо ви хочете зробити щось "приватним", воно не має бути видимим для сторонніх.

    ```javascript
    // погано
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // добре
    this.firstName = 'Panda';
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [22.5](#naming--self-this) Не зберігайте посиланнь на `this`. Використовуйте arrow-функції чи [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind). jscs: [`disallowNodeTypes`](http://jscs.info/rule/disallowNodeTypes)

    ```javascript
    // погано
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // погано
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // добре
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [22.6](#naming--filename-matches-export) Базове ім'я файлу має співпадати з експортом за замовчуванням.

    ```javascript
    // файл 1 містить
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // файл 2 містить
    export default function fortyTwo() { return 42; }

    // файл 3 містить
    export default function insideDirectory() {}

    // у якомусь іншому файлі
    // погано
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // погано
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // добре
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [22.7](#naming--camelCase-default-export) Використовуйте camelCase коли ви експортуєте за замовчуванням function. Ім'я файлу повинно співпадати з іменем функції.

    ```javascript
    function makeStyleGuide() {
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [22.8](#naming--PascalCase-singleton) Використовуйте PascalCase коли ви експортуєте конструктор / клас / функціональну бібліотеку / чистий об'єкт.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      }
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [22.9](#naming--Acronyms-and-Initialisms) Скорочення або абревіатури повинні завжди всі писатись або великими або маленькими літерами.

    > Чому? Імена для зручності читання, а не для вдоволення комп'ютерного алгоритму.

    ```javascript
    // погано
    import SmsContainer from './containers/SmsContainer';

    // погано
    const HttpRequests = [
      // ...
    ];

    // добре
    import SMSContainer from './containers/SMSContainer';

    // добре
    const HTTPRequests = [
      // ...
    ];

    // найкраще
    import TextMessageContainer from './containers/TextMessageContainer';

    // найкраще
    const Requests = [
      // ...
    ];
    ```

**[⬆ вверх](#Зміст)**


## Аксессори

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [23.1](#accessors--not-required) Функції аксессори для доступу до властивостей не потрібні.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [23.2](#accessors--no-getters-setters) Не використовуйте геттери/сеттери JavaScript оскільки вони викликають неочікуванні побічні ефекти і їх важко тестувати, підтримувати і аргументувати їхню необхідність. Натомість, якщо ви робити функцію доступу - використовуйте getVal() та setVal('hello').

    ```javascript
    // погано
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // добре
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [23.3](#accessors--boolean-prefix) Якщо властивість/метод являються `boolean`, використовуйте `isVal()` або `hasVal()`.

    ```javascript
    // погано
    if (!dragon.age()) {
      return false;
    }

    // добре
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [23.4](#accessors--consistent) Це нормально створювати get() та set() функції, але будьте послідовні.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ вверх](#Зміст)**


## Події

  <a name="events--hash"></a><a name="24.1"></a>
  - [24.1](#events--hash) Коли додаєте якусь інформацію до подій (неважливо до DOM подій, чи до якихось більш конкретних, наприклад подій у Backbone), передавайте хеш замість чистого значення. Це дозволяє в подальшому додавати більше даних до події без пошуку та оновлення кожного обробника події. Наприклад, замість:

    ```javascript
    // погано
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', (e, listingId) => {
      // зробити щось з listingId
    });
    ```

    віддати перевагу такому:

    ```javascript
    // добре
    $(this).trigger('listingUpdated', { listingId: listing.id });

    ...

    $(this).on('listingUpdated', (e, data) => {
      // зробити щось з data.listingId
    });
    ```

  **[⬆ вверх](#Зміст)**


## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [25.1](#jquery--dollar-prefix) Префіксуйте об'єкт jQuery знаком `$`. jscs: [`requireDollarBeforejQueryAssignment`](http://jscs.info/rule/requireDollarBeforejQueryAssignment)

    ```javascript
    // погано
    const sidebar = $('.sidebar');

    // добре
    const $sidebar = $('.sidebar');

    // добре
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [25.2](#jquery--cache) Кешуйте результати пошуку jQuery.

    ```javascript
    // погано
    function setSidebar() {
      $('.sidebar').hide();

      // ...щось відбувається...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // добре
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...щось відбувається...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [25.3](#jquery--queries) Для звернень до DOM використовуйте каскадність запиту `$('.sidebar ul')` або предок > нащадок `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [25.4](#jquery--find) Використовуйте `find` з контекстними запитами jQuery об'єкта.

    ```javascript
    // погано
    $('ul', '.sidebar').hide();

    // погано
    $('.sidebar').find('ul').hide();

    // добре
    $('.sidebar ul').hide();

    // добре
    $('.sidebar > ul').hide();

    // добре
    $sidebar.find('ul').hide();
    ```

**[⬆ вверх](#Зміст)**


## ECMAScript 5 сумісність

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [26.1](#es5-compat--kangax) Звертайтесь до ES5 [таблиці сумісності](https://kangax.github.io/es5-compat-table/) [Kangax](https://twitter.com/kangax/)'са.

**[⬆ вверх](#Зміст)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) стилі

  <a name="es6-styles"></a><a name="27.1"></a>
  - [27.1](#es6-styles) Це колекція посилання на різні особливості ES6.

1. [Arrow Functions](#arrow-функції)
1. [Класи та Конструктори](#Класи-та-Конструктори)
1. [Скорочення для методіва об'єкта](#es6-object-shorthand)
1. [Скорочення об'єкта](#es6-object-concise)
1. [Вираховані властивості об'єкта](#es6-computed-properties)
1. [Строчні шаблони](#es6-template-literals)
1. [Destructuring](#Деструктурування)
1. [Параметри за замовчуаванням](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [spreads оператор масива](#es6-array-spreads)
1. [Let та Const](#Посилання)
1. [Ітератори та Генератори](#Ітератори-та-генератори)
1. [Модулі](#Модулі)

  <a name="tc39-proposals"></a>
  - [27.2](#tc39-proposals) Не використовуйте [TC39 пропозиції](https://github.com/tc39/proposals) які не знаходяться у стадії stage 3.

    > Чому? [Вони не завершені](https://tc39.github.io/process-document/), і вони можуть бути змінені або повністю відмінені. Ми хочемо використовувати JavaScript, а пропозиції, покищо, ще не JavaScript.

**[⬆ вверх](#Зміст)**

## Тестування

  <a name="testing--yup"></a><a name="28.1"></a>
  - [28.1](#testing--yup) **Так.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [28.2](#testing--for-real) **Ні, але серйозно**:
   - Який би тестувальний фреймфорк ви б не використовували - ви повинні писати тести!
   - Намагайтесь писати багато дрібних функцій та зводити до мінімуму місця, де відбуваються мутації.
   - Будьте обережними з stubs та mocks, оскільки вони можуть зробити ваші тести більш крихкими.
   - Ми в першу чергу використовуємо [`mocha`](https://www.npmjs.com/package/mocha) у Airbnb. [`tape`](https://www.npmjs.com/package/tape) також час від часу використовується для малньких, окремих модулів.
   - 100% покриття тестами - це гарна мета до якої варто прагнути, навіть якщо це не завжди практично.
   - Кожного разу, коли ви виправляєте помилку, _пишіть тест регресії_. Помилка виправлена без написання регресивного тесту майже точно виникне в майбутньому знову.

**[⬆ вверх](#Зміст)**


## Продуктивність

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat)
  - [Are Javascript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ вверх](#Зміст)**


## Ресурси

**Вивчення ES6**

  - [Draft ECMA 2015 (ES6) Spec](https://people.mozilla.org/~jorendorff/es6-draft.html)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Прочитайте це**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Інструменти**

  - Code Style Linters
    + [ESlint](http://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    + [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
    + [JSCS](https://github.com/jscs-dev/node-jscs) - [Airbnb Style Preset](https://github.com/jscs-dev/node-jscs/blob/master/presets/airbnb.json)

**Інші керівництва**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)

**Інші стилі**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Подальше читання**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Книжки**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don't Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Блоги**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [Dustin Diaz](http://dustindiaz.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Подкасти**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)


**[⬆ вверх](#Зміст)**

## В реальному Світі

  Це перелік організацій які використовують це керівництво. Надішліть нам pull request і ми додамо вас до цього списку.

  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Adult Swim**: [adult-swim/javascript](https://github.com/adult-swim/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avalara**: [avalara/javascript](https://github.com/avalara/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **BashPros**: [BashPros/javascript](https://github.com/BashPros/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk/javascript](https://github.com/Bisk/javascript/)
  - **Blendle**: [blendle/javascript](https://github.com/blendle/javascript)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Expensify** [Expensify/Style-Guide](https://github.com/Expensify/Style-Guide/blob/master/javascript.md)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia/javascript](https://github.com/gawkermedia/javascript)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **Huballin**: [huballin/javascript](https://github.com/huballin/javascript)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InfoJobs**: [InfoJobs/JavaScript-Style-Guide](https://github.com/InfoJobs/JavaScript-Style-Guide)
  - **Intent Media**: [intentmedia/javascript](https://github.com/intentmedia/javascript)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://github.com/kesne/jeopardy-bot/blob/master/STYLEGUIDE.md)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **KickorStick**: [kickorstick/javascript](https://github.com/kickorstick/javascript)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **ModCloth**: [modcloth/javascript](https://github.com/modcloth/javascript)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://github.com/moneyadviceservice/javascript)
  - **Muber**: [muber/javascript](https://github.com/muber/javascript)
  - **National Geographic**: [natgeo/javascript](https://github.com/natgeo/javascript)
  - **National Park Service**: [nationalparkservice/javascript](https://github.com/nationalparkservice/javascript)
  - **Nimbl3**: [nimbl3/javascript](https://github.com/nimbl3/javascript)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Razorfish**: [razorfish/javascript-style-guide](https://github.com/razorfish/javascript-style-guide)
  - **reddit**: [reddit/styleguide/javascript](https://github.com/reddit/styleguide/tree/master/javascript)
  - **React**: [/facebook/react/blob/master/CONTRIBUTING.md#style-guide](https://github.com/facebook/react/blob/master/CONTRIBUTING.md#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/blob/master/docs/javascript.md)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://github.com/seekingalpha/javascript-style-guide)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Springload**: [springload/javascript](https://github.com/springload/javascript)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ вверх](#Зміст)**

## Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [sivan/javascript-style-guide](https://github.com/sivan/javascript-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [tipjs/javascript-style-guide](https://github.com/tipjs/javascript-style-guide)
  - ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [mjurczyk/javascript](https://github.com/mjurczyk/javascript)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [uprock/javascript](https://github.com/uprock/javascript)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [hngiang/javascript-style-guide](https://github.com/hngiang/javascript-style-guide)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)


## License

(The MIT License)

Copyright (c) 2014-2016 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ вверх](#Зміст)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
