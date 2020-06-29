# NOTFLIX (React JS Basic)

## 1. Fundamentals

> [MDN|JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript)

### # 1.0 Introduction

- Requirements (Concepts)
  - arrow function
  - spread operator
  - class
  - array operation

### # 1.1 Arrow Functions

-  normal function

  ```react
  function sayHello(name) {
    return `Hello ${name}`;
  }
  
  const kenny = sayHello("kenny");
  
  console.log(kenny);
  
  // result
  Hello kenny 
  ```

- arrow function
  ```react
  const sayHello = name => `Hello ${name}`;
  
  const kenny = sayHello("kenny");
  
  console.log(kenny);
  
  // result
  Hello kenny 
  ```

  - `const` 로 정의하는 문장 안에 arrow function 을 위치

  - `{ }` 의 유무

    - 만약 `{ }` 이 있다면 `{ }`내에 return 문이 나올 것임을 뜻한다

      ```react
      const sayHello = name => {
       return `Hello ${name}`   
      };
      ```

    - 만약 `{ }` 이 없다면 `=>` 뒤에 오는 내용 자체가 return 될 것임을 뜻한다

      ```react
      const sayHello = name => `Hello ${name}`;
      ```

  - event 추가, anonymous function 생성 등에 유용

    - normal

      ```js
      button.addEventListener("click", function(event) {
        console.log(event)
      });
      ```

    - arrow

      ```js
      button.addEventListener("click", event => console.log(event));
      ```

  - `( )` 의 유무

    - 만약 arrow function의 argument 가 하나라면 괄호를 사용할 필요 없다

    - arguments 가 두개 이상이라면 괄호를 사용해야 한다

      ```js
      const sayHello = (name1, name2) => `Hello ${name1} and ${name2}`;
      ```

- default value

  - normal / arrow 상관 없이, 추가된 내용

  - 정의 시에 `=` 를 활용해 default value 를 줄 수 있다

    ```react
    // normal function
    function sayHello(name = 'kenny') {
      return `Hello ${name}`;
    }
    
    // arrow function
    const sayHello = (name = 'kenny') => `Hello ${name}`;
    ```

  - default value 를 주지 않은 함수에서, 인자를 넘겨주지 않는 경우 `undefined`가 된다

    ```react
    const sayHello = name => `Hello ${name}`;
    
    const kenny = sayHello();
    
    console.log(kenny);
    
    // result
    Hello undefined
    ```

### # 1.2 Template Literals

- template literals

  - variable을 사용한 string을 편하게 만드는 방법

  - **`**  (backtick) 과 `${variable}` 을 사용

    ```js
    const name = 'kenny'
    
    console.log(`Hello ${name}`)
    ```

### # 1.3 Object Destructuring

- normal way

  ```js
  const human = {
    name: 'Kenny',
    lastName: 'Cha',
    nationality: 'Korean'
  }
  
  const name = human.name
  const lastName = human.lastName
  const nationality = human.nationality
  
  console.log(name, lastName, nationality)
  ```

- destructuring

  - object에 기반해서 variable들을 편하게 정의하는 방법

    ```js
    const human = {
      name: 'Kenny',
      lastName: 'Cha',
      nationality: 'Korean'
    }
    
    const { name, lastName, nationality } = human;
    
    console.log(name, lastName, nationality);
    ```

  - `:` 을 사용해서 variable name을 object key와 다르게 정의할 수 있다

    ```js
    const human = {
      name: 'Kenny',
      lastName: 'Cha',
      nationality: 'Korean'
    }
    
    const { name, lastName, nationality: diffName } = human;
    
    console.log(name, lastName, diffName);
    ```

  - `: {}`를 사용해 더 깊은 depth로 들어갈 수도 있다

    ```js
    const human = {
      name: "Kenny",
      lastName: "Cha",
      nationality: "Korean",
      todayMeals: {
        breakfast: "Samgyupsal",
        lunch: "Pasta",
        dinner: "Chicken"
      }
    };
    
    const {
      name,
      lastName,
      nationality: diffName,
      todayMeals: { breakfast, lunch, dinner }
    } = human;
    
    console.log(name, lastName, diffName, breakfast, lunch, dinner);
    ```

### # 1.4 Spread Operator

- wrong ways

  ```js
  const days = ["Mon", "Tues", "Wed"];
  const otherDays = ["Thu", "Fri", "Sat"];
  
  const allDays1 = days + otherDays;
  
  console.log(allDays1);
  
  // result (string)
  Mon,Tues,WedThu,Fri,Sat
  
  const allDays2 = [days + otherDays];
  
  console.log(allDays2);
  
  // result (array with 1 str item)
  ['Mon,Tues,WedThu,Fri,Sat']
  ```

  - `allDays1` 의 경우, 결과물이 array가 아니라 string으로 나오기 때문에, 개별 접근/ 순회 등의 기능을 사용할 수 없다
  - `allDays2` 또한 원하는 결과와 다르다

- spread operator with array

  ```js
  const days = ["Mon", "Tues", "Wed"];
  const otherDays = ["Thu", "Fri", "Sat"];
  
  // const allDays = days + otherDays;
  
  const allDays = [...days, ...otherDays, "Sun"];
  
  console.log(allDays);
  
  // result
  ["Mon", "Tues", "Wed", "Thu", "Fri", "Sat", "Sun"]
  ```

  - `...` 을 array 앞에 붙여, array로부터 item들을 가져와서 unpack

- spread operator with object

  ```js
  const ob = {
    first: "hi",
    second: "hello"
  };
  
  const ab = {
    third: "bye"
  };
  
  const two = { ...ob, ...ab };
  
  console.log(two);
  
  // result
  Object {first: "hi", second: "hello", third: "bye"}
  ```

  - object에서도 동일하게 사용 가능하다

### # 1.5 Classes

- programming paradigm
  - Functional programming
  - Object-Oriented Programming (OOP)

- Classes

  ```js
  class Human {
    constructor(name, lastName) {
      this.name = name;
      this.lastName = lastName;
    }
  }
  
  const kenny = new Human("kenny", "cha");
  
  console.log(kenny);
  console.log(kenny.name);
  
  // result
  Human {name: "kenny", lastName: "cha", constructor: Object}
  kenny
  
  class Baby extends Human {
    cry() {
      console.log("Waaaa");
    }
    sayName() {
      console.log(`My name is ${this.name}`);
    }
  }
  
  const myBaby = new Baby("mini", "me");
  
  console.log(myBaby);
  myBaby.cry();
  myBaby.sayName();
  
  // result
  Baby {name: "mini", lastName: "me", constructor: Object}
  Waaaa 
  My name is mini 
  ```

  - `constructor`
    - 클래스 객체 생성 시 호출되는 method
  - `new` 
    - `new ClassName(args) ` 의 형식으로 객체 생성
  - `extends`
    - 클래스 확장(상속)
    - 특히 react의 component들은 Class이기 때문에 `extends` 활용 빈도가 높다
  - `this`
    - Class 정의 내에서의 this는 현재 Class 자체를 의미 (python의 self와 유사)

### # 1.6 Array map

- map

  ```js
  const days = ["Mon", "Tue", "Wed", "Thu", "Fri"];
  
  const smilingDays = days.map(day => `${day}😀`);
  
  console.log(smilingDays);
  
  // result
  ["Mon😀", "Tue😀", "Wed😀", "Thu😀", "Fri😀"]
  ```

  - 배열의 모든 item들에 function을 실행하고, 그 결과값으로 새로운 배열을 만드는 method

  - 외부에 callback function 정의 후 호출하는 방식으로도 가능

    ```js
    const days = ["Mon", "Tue", "Wed", "Thu", "Fri"];
    
    const addSmile = day => `${day}😀`
    
    const smilingDays = days.map(addSmile);
    
    console.log(smilingDays);
    
    // result
    ["Mon😀", "Tue😀", "Wed😀", "Thu😀", "Fri😀"]
    ```

    - 코드 수정 및 재사용에 편리한 방식

  - `map` method의 두번째 인자(index)

    ```js
    const days = ["Mon", "Tue", "Wed", "Thu", "Fri"];
    
    const smilingDays = days.map((day, index) => `#${index} ${day}😀`);
    
    console.log(smilingDays);
    
    // result
    ["#0 Mon😀", "#1 Tue😀", "#2 Wed😀", "#3 Thu😀", "#4 Fri😀"]
    ```

    - array의 각 item들의 index

### # 1.7 Array filter

- filter

  ```js
  const numbers = [2, 45, 12, 31, 5424, 123, 356, 3, 12, 44, 5];
  
  const biggerThanFifteen = numbers.filter(number => number > 15);
  
  console.log(biggerThanFifteen);
  
  // result
  [45, 31, 5424, 123, 356, 44]
  ```

  - array의 item 중 test function을 통과한 item들을 모아서 새로운 배열을 만드는 method

  - 외부에 callback function 정의 후 호출하는 방식

    ```js
    const numbers = [2, 45, 12, 31, 5424, 123, 356, 3, 12, 44, 5];
    
    const testCondition = number => number > 15;
    
    const biggerThanFifteen = numbers.filter(testCondition);
    
    console.log(biggerThanFifteen);
    ```

### # 1.8 forEach / push / includes

- forEach

  ```js
  const posts = ["h1", "hello", "bye"];
  
  posts.forEach(post => console.log(post));
  
  // result
  h1 
  hello 
  bye 
  ```

  - array의 item 각각에 대해 function을 시행
    - return 하지 않음

- push

  ```js
  const posts = ["h1", "hello", "bye"];
  
  posts.push("new");
  
  console.log(posts);
  
  // result
  ["h1", "hello", "bye", "new"]
  ```

  - array에 새로운 item을 추가

- includes

  ```js
  const greetings = ["h1", "howdy", "suup"];
  
  if (!greetings.includes("hello")) {
    greetings.push("hello");
  }
  
  console.log(greetings);
  
  // result
  ["h1", "howdy", "suup", "hello"]
  ```

  - 특정 item을 array가 포함하는지 체크

- reverse

  ```js
  const greetings = ["h1", "howdy", "suup"];
  
  greetings.reverse();
  
  console.log(greetings);
  
  // result 
  ["suup", "howdy", "h1"]
  ```

  - array 순서 반전

- sort

  ```js
  const numbers = [1, 4, 3, 2, 5];
  
  numbers.sort();
  
  console.log(numbers);
  
  // result 
  [1, 2, 3, 4, 5]
  ```

  - array 정렬

## 2. Project Setup

### # 2.0 Setting up the project

- create-react-app

  - npx

    ```bash
    # npx 설치
    $ npm - npx -g
    # npx를 통해 create-react-app 실행
    $ npx create-react-app notflix
```
    
- 사용되지 않는 지나간 버전의 패키지들을 컴퓨터에 저장하지 않기위해 사용
    - npx를 통해 최신버전의 create-react-app을 설치해 실행하고, 끝나면 컴퓨터에서 삭제
  
- jsconfig.json

  ```json
  {
    "compilerOptions": {
      "baseUrl": "src"
    },
    "include": ["src"]
  }
  ```

  - root path setting
    - for absolute imports
    - [create-react-app|absolute imports](https://create-react-app.dev/docs/importing-a-component/#absolute-imports)

- prop-types

  ```bash
  $ npm i prop-types
  ```

  - 전달받은 데이터 유효성 검증을 위한 패키지