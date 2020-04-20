## 노마드 React

### 1. 사용하기에 앞서 설치가 필요한 것들 / 알아야 하는 것들

- nodeJS, npm, npx, git, VSC

- HTML / CSS / 바닐라 JS 

  - const, let, function(args), array, object

- 리액트는 페이스북에서 만들었다.

  - 에어비앤비, npm, neflix, sportify, slack 등등..

  - object, class, function, variavles등등 자바스크립트로 이루어져 있다.

### 2. Creating your First React App

- 리액트를 사용하기 위해선 web pack, babel을 받아야 한다.

  - 컴포넌트 단위로 세련되게 작성한 코드가 브라우저 상에서 해석하지 못해서, 위의 webpack, babel을 사용해서 구스타일의 자바스크립트 코드로 변환해줘야 한다.

  - 리액트 코드를 컴파일 하고, 다른 파일을 넣어야 하고, 그 다음 또 다른 작업이 필요하다. (이 작업을 babel, webpack을 사용한다.)
  
1. 설치

- npx create-react-app movie_app_ohmy0418_2019

      Success! Created movie_app_ohmy0418_2019 at /Users/nathalie/Documents/movie_app_ohmy0418_2019
      Inside that directory, you can run several commands:

        yarn start (npm)
          Starts the development server.

        yarn build (npm)
          Bundles the app into static files for production.

        yarn test (npm)
          Starts the test runner.

        yarn eject (npm)
          Removes this tool and copies build dependencies, configuration files
          and scripts into the app directory. If you do this, you can’t go back!

      We suggest that you begin by typing:

        cd movie_app_ohmy0418_2019
        yarn start

      Happy hacking

- npm start 하면 새창이 뜨고, 터미널에서 다음과 같은 내용이 뜬다.

          Local:            http://localhost:3000/ - 내 로컬 
          On Your Network:  http://172.28.31.248:3000/ - WIFI [wi-fi에 친구가 있거나, 폰에 테스트를 하고 싶을 때, 이 링크를 사용한다.

  2. 리액트가 작동하는 방식

  - virtual DOM (virtual document object model)
  
    - react는 소스코드에 처음부터 HTML을 넣지 않고, HTML에서 HTML을 추가하거나 제거하는 법을 알고 있다. 그래서 application이 이것을 로드한 다음, react가 작성해둔 component를 HTML을 멀어넣게 되는 것이다.

  -  component - HTML을 반환하는 함수이다.

    - ReactDOM.render(<App />, document.getElementById('potato'));

    - JS + HTML 의 조합 = JSX 

      - JSX 에서 HTML 사용할 때, class => className 과 같이 속성이 약간씩 다르다.

### 3. 작업 Link 및 CHECk

- https://ohmy0418.github.io/movie_app_ohmy0418_2019

1. 시작과 끝

  - 시작 

    - import React from "react"

    - import PropTypes from "prop-types";

  - 끝 - export default App; (함수 컴포넌트 불러오기)

2. 주요 설치하는 API / 유용한 정보

  - npm i prop-types : 내가 picture를 불러와야 하는데, 실수로 image로 입력하는 경우, 등 사람이 실수할 수 있는 부분에 대해서 바로잡아 주는 기능, 내가 전달받은 props가, 내가 원하는 props인지를 확인해 주는 것 

        사용 예시

        Food.propTypes = {
          name:PropTypes.string.isRequired,
          picture:PropTypes.string.isRequired,
        }

  - class Component의 사용

    - function Component는 return을 요구하지만, class Component는 render를 요구한다.
  
    - state의 사용

      - state는 Object 형태이고, component의 데이터를 넣을 수 있으며, 이 데이터는 이벤트에따라 변한다.

      - react의 render를 refresh 하지 않는다. 즉, 매번 state의 상태를 변경할 때, react가 render function을 호출해서 바꿔주길 원한다 ===> setState를 사용한다.

            state = {
              count : 0;
            }

    - setState

      - setState를 호출하면, react는 state를 resrech 하고, render function도 호출한다.

      - html 개발자 도구를 확인하면, virtual DOM을 가지고 있기 때문에, 빠르게 변경이 가능하고 깜박거리는 현상도 없이, 바뀌는 부분만 변화한다.

      - state와 함께, setState를 사용하지 않으면, 새 state와 함께 render function이 호출되지 않는다.

            사용 예시

            add = () => {
              this.setState(current => 
                (
                  {count : current.count + 1 }
                )
              );
            }

    - componentDidMount : component가 처음 render 됐다고 알려주는 것 (render 후에 보인다)

          사용 예시

            componentDidMount(){
              console.log("componentDidMount");
            }

    - componentDidUpdate : 버튼을 클릭하거나, 어떠한 동작을 발생하면 console에서 나타난다. (setState를 호출하면, component가 호출되고, render를 호출한 다음에, 업데이트가 완료되면 componentDidUpdate가 실행된다.)

          사용 예시

          componentDidUpdate(){
            console.log("I Just Updated")
          }

    - componentWillUnmount : component가 떠날 때 호출한다. (다른 페이지로 이동하거나 등등)

    - constructor() : JS에서 나오는 것
    
    - component가 mounting 될 때, component가 screen에 표시될 때, component가 website에 들어갈 때, constrctor를 호출한다. ==> 그 다음, render가 호출된다. ==> 그 다음, componentDidMount가 호출된다.

    - mounting : 태어나는 것

    - updating : 업데이트 => 버튼 클릭 시 발생하는 이벤트와 같이 state를 변경할 때, 그것이 업데이트 다.

    - unmounting : component가 dead (페이지를 바꾸거나, 교체할 경우)

    

  

        


      


