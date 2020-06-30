# NOTFLIX (React JS Basic)

## 0. Notflix

> Learning React and ES6 by building a Movie Discovery App.

### # 0.1 Screens

- [ ] Home
- [ ] TV Shows
- [ ] Search
- [ ] Detail

### # 0.2 API Verbs

- [x] Now playing (Movie)
- [x] Upcoming (Movie)
- [x] Top Rated (TV)
- [x] Popular (TV, Movie)
- [x] Search (TV, Movie)
- [x] Airing Today (TV)
- [x] TV Show Detail
- [x] Movie Detail

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
### # 2.1~2.2 React Router

- change `src` structure

  - `src/ Components/`  폴더를 만든 후 App.js 를 안으로 이동

    - 이때, jsconfig.json 의 설정 때문에, index.js에서 App 을 import 해올 때 아래와 같이 절대경로로 import 가능

    ```react
    // 기존
    import App from './Components/App'
    
    // absolute import
    import App from 'Components/App';
    ```

  - `src/ Routes/` 폴더 생성 

    - 필요한 screen별로 .js 파일 생성

    ```react
    // Home.js TV.js Search.js Detail.js
    
    export default () => 'Home'
    ```

- react-router

  - [github|react-router](https://github.com/ReactTraining/react-router)

  - [Doc|react-router-dom](https://reacttraining.com/react-router/web/guides/quick-start)

  - 설치

    ```bash
    $ npm i react-router-dom
    ```

  - 사용

    ```react
    // src/Components/App.js
    
    import React, { Component } from 'react';
    import Router from 'Components/Router'
    
    class App extends Component {
      render() {
        return (
          <>
            <Router />
          </>
        );  
      }
    }
    
    export default App;
    ```

    ```react
    // src/Components/Router.js
    
    import React from 'react'
    import { HashRouter as Router, Route } from 'react-router-dom'
    import Home from 'Routes/Home'
    import TV from 'Routes/TV'
    import Search from 'Routes/Search'
    
    export default () => (
      <Router>
        <Route path="/" exact component={Home} />
        <Route path="/tv" exact component={TV} />
        <Route path="/search" component={Search} />
      </Router>
    )
    ```

    - `Components/ Router.js` 파일 생성
    - Router.js 파일에서 Router내에 각 screen 별 Route를 생성하고, Route마다 각 path별로 component들을 연결
    - App.js 파일에서 Router를 import 한 후 사용

  - HashRouter
    - `http://localhost:3000/#/search` 와 같이 root에 `/#/` 이 붙은 url 생성
    - BrowserRouter와 같은 기능을 하지만, 가운데에 `#` 이 있어 웹사이트 보다는 앱에 있다는 느낌을 준다
    - HashRouter는 URL의 hash portion을, BrowserRouter는 HTML5 history API를 사용

  - Fragments

    - React에서는 하나의 Component만을 return 할 수 있다
    - 때문에, `<> </> (Fragments)`를 사용해서 여러개의 Component를 return한다
    - key가 있는 경우, `React.Fragment`를 명시적으로 사용해야 하며, 단축문법인 <></>를 사용할 수 없다

  - Composition

    ```react
    <Router>
        <Route path="/tv" exact component={TV} />
        <Route path="/tv/popular" render={() => <h1>Popular</h1>} />
      </Router>
    ```

    - 두개 이상의 Route를 동시에 render 하는 방식
    - exact가 없는 상태에서 `/tv/popular` 에 두개의 Route가 모두 해당하기 때문에, 둘을 동시에 render한다

  - Switch

    ```react
    import { Switch } from 'react-router-dom'
    
    export default () => (
      <Router>
        <Switch>
          <Route path="/tv" exact component={TV} />
          <Route path="/tv/popular" render={() => <h1>Popular</h1>} />
        </Switch>
      </Router>
    )
    
    ```

    - 한 번에 오직 하나의 Route만 render하도록 만든다
    - `http://localhost:3000/tv/popular` 로 이동하면 ,`/tv` 에 해당하는 component는 render 되지 않고, `/tv/popular` 에 해당하는 내용만 render 된다

  - Redirect

    ```react
    import { Redirect } from 'react-router-dom'
    
    export default () => (
      <Router>
        <Route path="/" exact component={Home} />
        <Route path="/tv" exact component={TV} />
        <Route path="/tv/popular" render={() => <h1>Popular</h1>} />
        <Route path="/search" component={Search} />
        <Redirect from="*" to="/" />
      </Router>
    )
    ```

    - 현재 url이 어느 Route의 path에도 해당되지 않는다면, Redirect의 to 에 해당하는 주소로 이동

## 3. Styles

### # 3.0~3.2 CSS in React

- options of styling css in react

  - use `styles.css`

    - 간단하지만, Component와 css 가 분리되어 있음

  - make each `Component's folder`

    - 각 Component 별로 폴더를 만들고, 아래와 같이 파일 구성

      ```
      # src/Components/ExampleComponent/
      
      index.js
      ExampleComponent.js
      ExampleComponent.css
      ```

    - 폴더를 만들어야 하고, 매번 css 파일을 import 해야 하고, 여전히 className을 기억해야 한다

  - use `CSS module ` (or scss)

    ```css
    /* Header.module.css */
    
    .navList {
      display: flex;
    }
    
    .navList:hover {
      background-color: blue;
    }
    ```

    ```react
    // Header.js
    
    import styles from './ExampleComponent.module.css'
    
    export default () => (
      <header>
        <ul className={styles.navList}>
          <li>
            <a href="/">Movies</a>
          </li>
        </ul>  
      </header>
    )
    ```

    - css 파일명을 `ExampleComponent.module.css` 로 하고, js 파일과 같은 방식으로 import 한 후, object와 비슷한 방식으로 사용
    - 임의화 되어 더 안전해졌지만, 여전히 js와 css는 분리되어 있고, className을 기억해야 한다는 불편함

  - styled-components

- styled-components

  - 설치

    ```bash
    $ npm i styled-components
    ```

  - 사용

    ```react
    import React from 'react'
    import { Link } from 'react-router-dom'
    import styled from 'styled-components'
    
    const Header = styled.header`
    `
    const List = styled.ul`
      display: flex;
      &:hover {
        background-color: blue;
      }
    `
    const Item = styled.li`
    `
    const SLink = styled(Link)`
    `
    
    export default () => (
      <Header>
        <List>
          <Item>
            <SLink to="/">Movies</SLink>
          </Item>
          <Item>
            <SLink to="/tv">TV</SLink>
          </Item>
          <Item>
            <SLink to="/search">Search</SLink>
          </Item>
        </List>
      </Header>
    )
    ```

    - styled.elementName\`cssInformation\` 의 구조로 styled-component 정의한 후 사용
    -  `Link` 는 JavaScript 방식으로 이동하도록 한다 (`a` 는 브라우저 방식)

### # 3.3 GlobalStyle and Header

- `createGlobalStyle`

  ```react
  import { createGlobalStyles } from 'styled-components'
  import reset from 'styled-reset'
  
  const globalStyles = createGlobalStyle`
    ${reset};
    a {
      text-decoration: none;
      color: inherit;
    }
    * {
      box-sizing: border-box;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
      font=size: 14px;
      background-color: rgba(20, 20, 20, 1);
    }
  `
  
  export default globalStyles
  ```

  - `src/ Components/ GlobalStyles.js` 파일을 생성한 후 전체에 사용할 css 정의

  - styled-reset

    - styled-components를 활용해 css를 초기화하는 패키지

      ```bash
      # 설치
      $ npm i styled-reset
      ```

      ```react
      // import 한 후 GlobalStyles에 사용
      // css 가장 윗 줄에 작성
      import reset from 'styled-reset'
      
      const globalStyles = createGlobalStyle`
        ${reset};
      `
      ```

### # 3.4 Location Aware Header

- `props` of styled-components

  ```react
  import { withRouter } from 'react-router-dom'
  
  const Item = styled.li`
    border-bottom: 3px solid ${props => props.current ? "#3498db" : "transparent"};
    transition: border-bottom 0.5s ease-in-out;
  `
  
  export default withRouter(({location: { pathname }}) => (
    <Header>
      <List>
        <Item current={pathname === "/"}>
          <SLink to="/">Movies</SLink>
        </Item>
        <Item current={pathname === "/tv"}>
          <SLink to="/tv">TV</SLink>
        </Item>
        <Item current={pathname === "/search"}>
          <SLink to="/search">Search</SLink>
        </Item>
      </List>
    </Header>
  ))
  ```

  - props

    - `props.location.pathname` 에 해당하는 data를 object destructuring를 사용해서 불러온다
    - 불러온 pathname에 해당하는 Item에 대해서만 `current=true` 가 된다
    - styled-component 정의 과정에서 3항 연산자를 통해 current=true 일 때만 아래쪽 테두리를 준다

  - withRouter

    - [react-router|withRouter](https://reacttraining.com/react-router/core/api/withRouter)
    - 다른 component를 감싸는 component
    - withRouter로 감싸면 props를 사용할 수 있게 된다

    ```react
    export default withRouter(props => (
      <Header>
        {console.log(props)}
      </Header>
    ))
    
    // result
    {
      history: {length: 23, action: "POP", location: {…}, createHref: ƒ, push: ƒ, …}
      location: {pathname: "/", search: "", hash: "", state: undefined, key: "12gipr"}
      match: {path: "/", url: "/", params: {…}, isExact: true}
      staticContext: undefined
      __proto__: Object
    }
    ```


## 4. Networking

### # 4.0 Introduction to The Movie DB API

- The Movie DB
  - [TMDB|API doc](https://developers.themoviedb.org/3)

### # 4.1 Sexy Networking with Axios instances

- `src/ api.js` 파일 생성

  - axios instance 를 만들어서 사용

  ```react
  import axios from 'axios'
  
  const api = axios.create({
    baseURL: "https://api.themoviedb.org/3/",
    params: {
      api_key: "44084423a3ad71eb2acee3298e9a25e8",
      language: "en-US"
    }
  })
  
  export default api
  ```

  - network와 api에 관한 내용만 작성

- axios

  - [github|axios](https://github.com/axios/axios)

    - a package needed to fetch

  - [axios|create an instance](https://github.com/axios/axios)

    - create a new instance of axios with a custom config

      ```react
      const instance = axios.create({
        baseURL: 'https://some-domain.com/api/',
        timeout: 1000,
        headers: {'X-Custom-Header': 'foobar'}
      });
      ```

  - 설치

    ```bash
    $ npm i axios
    ```

  - 사용

    ```react
    import axios from 'axios'
    ```

### # 4.2~4.3 API Verbs

- moviesApi / tvApi

  ```react
  import axios from 'axios'
  
  const api = axios.create({
    baseURL: "https://api.themoviedb.org/3/",
    params: {
      api_key: "44084423a3ad71eb2acee3298e9a25e8",
      language: "en-US"
    }
  })
  
  export const moviesApi = {
    nowPlaying: () => api.get("movie/now_playing"),
    upcoming: () => api.get("movie/upcoming"),
    popular: () => api.get("movie/popular"),
    movieDetail: (id) => api.get(`movie/${id}`, {
      params: {
        append_to_response: "videos"
      }
    }),
    search: (term) => api.get("search/movie", {
      params: {
        query: encodeURIComponent(term)
      }
    })
  }
  
  export const tvApi = {
    topRated: () => api.get("tv/top_rated"),
    popular: () => api.get("tv/popular"),
    airingToday: () => api.get("tv/airing_today"),
    showDetail: (id) => api.get(`tv/${id}`, {
      params: {
        append_to_response: "videos"
      }
    }),
    search: (term) => api.get("search/tv", {
      params: {
        query: encodeURIComponent(term)
      }
    })
  }
  ```

  - axios instance를 통해 기본 요청 세팅을 하고, movie와 tv에 대해 각각 api verbs를 담은 object를 정의한 후 export

  - append_to_response

    - [TMDB|append to response](https://developers.themoviedb.org/3/getting-started/append-to-response)
    - 개별 movie 나 tv show에 대한 videos, images 를 더해 주는 것

  - encoding URI

    ```react
    search: (term) => api.get("search/movie", {
      params: {
        query: encodeURIComponent(term)
      }
    })
    ```

    - 특수문자 등에 대비한 encoding URI 
    - 문자열로 변환한 후 검색하기 위함

## 5. Containers

### # 5.0~5.1 Container Presenter Pattern

- Container-Presenter Pattern

  - [medium|presentational and container components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
  - [번역|presentational and container components](https://blueshw.github.io/2017/06/26/presentaional-component-container-component/)
  - 각 component를 container와 presenter로 나눈 후
    - data 및 logic은 container에
    - 보여지는 부분은 presenter에 작성

- HomeComponent (`src/ Routes/ Home/`)

  - index.js

    ```react
    import HomeContainer from './HomeContainer'
    
    export default HomeContainer
    ```

  - HomePresenter

    ```react
    export default () => "Home"
    ```

  - HomeContainer

    ```react
    import React, { Component } from 'react'
    import HomePresenter from './HomePresenter'
    
    export default class extends Component {
      state = {
        nowPlaying: null,
        upcoming: null,
        popular: null,
        error: null,
        loading: true
      }
      render() {
        const { nowPlaying, upcoming, popular, error, loading } = this.state
        return (
          <HomePresenter 
            nowPlaying={nowPlaying}
            upcoming={upcoming}
            popular={popular} 
            error={error}
            loading={loading}
          />
        )
      }
    }
    ```

### # 5.2 Home Container

- home container

  ```react
  import React, { Component } from 'react'
  import HomePresenter from './HomePresenter'
  // 외부에 따로 정의한 api 파일을 가져와 요청
  import { moviesApi } from 'api'
  
  export default class extends Component {
    // state 초기화
    state = {
      nowPlaying: null,
      upcoming: null,
      popular: null,
      loading: true,
      error: null
    }
    // 비동기작업이 일어날 대상
    async componentDidMount() {
      try {
        // await 가 붙은 부분에서 기다린다
        // object destruncturing을 통해 변수 정의
        const { data: { results: nowPlaying }} = await moviesApi.nowPlaying()
        const { data: { results: upcoming }} = await moviesApi.upcoming()
        const { data: { results: popular }} = await moviesApi.popular()
        this.setState({
          // object를 같은 이름으로 set하는 경우 아래와 같이 단축 가능
          nowPlaying, 
          upcoming,
          popular
        })
      } catch {
        this.setState({
          error: "Can't find movies information."
        })
      } finally {
        // error 발생 여부와 상관없이 loading이 끝났음을 표시
        this.setState({
          loading: false
        })
      }
    }
  
    render() {
      const { nowPlaying, upcoming, popular, loading, error } = this.state
      console.log(this.state)
      return (
        <HomePresenter 
          nowPlaying={nowPlaying}
          upcoming={upcoming}
          popular={popular} 
          loading={loading}
          error={error}
        />
      )
    }
  }
  ```

  - [axios|issue with merging params](https://github.com/axios/axios/issues/2190)

    - 최신 버전 axios에서 axios instance의 params가 자동으로 merge 되지 않는 이슈

    - 0.18.1 버전으로 다운그레이드 하면 해결

      ```bash
      # install package with version
      $ npm install axios@0.18.1
      ```

  - async & await

    - 비동기작업을 위해 사용

  - throw Error

    - error 를 발생시킴

      ```react
      throw Error()
      ```

      