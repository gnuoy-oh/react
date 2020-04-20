## 다양한 프론트엔드 라이브러리

#### 웹 뿐만이 아니라, 다양한 웹 애플리케이션이 생기면서 프론트엔드 라이브러리가 중요해졌다. 
    
* 프로젝트가 커지면 다양한 DOM 관리와 상태값 업데이트 관리를 최소한으로 하고, 오직 기능 개발, 사용자 인터페이스 구현을 집중할 수 있도록 많은 라이브러리나 프레임워크들이 만들어졌다. 이는 더 나은 유지보수를 위한 목적에도 관계가 있다. 

* angular , vue , react , backbone 등 다양하다.

    1. angular
    
        - 다양한 기능이 내장되어 있다.
        - http 클라이언트, 다국어지원 등 다 내장되어 있음
        - angular1 , angular new 
        - 프레임워크 차원에서 성숙하기는 하지만, 새로운 버전의 앵귤러로 인지도는 아직 성장하는 중이다.
        - 타입스크립트 사용이 필수이다
            
    2. vue
    
        - 입문자가 사용하기 가장 쉬운, cdn을 불러와서 사용하는 아주 쉬운 라이브러리
        - html을 템플릿처럼 그대로 사용할 수 있다.
        - 공식 라우터와 공식 상태 라이브러리가 존재한다.
        - 앵귤러처럼 디렉티브라는 기능이 있고, 리엑트처럼 버츄얼 돔 컴포넌트 기반도 있다.

    3. react
    
        - 컴포넌트 라는 개념이 집중되어있는 라이브러리
        - 컴포넌트 ? 데이터를 넣으면 지정한 인터페이스를 조립해서 보여주는 것
        - 페이스북 개발자들이 제작한 라이브러리
        - 공식 라이브러리의 개념이 없다.
        
## React

#### 지속해서 데이터가 변화하는 대규모 애플리케이션을 구축하기 위해 리액트를 만들었습니다. 
    
* 프레임워크 들은 데이터 단을 담당하는 Model, 사용자의 화면에서 보여지게 되는 View, 사용자가 발생시키는 이벤트 처리를 해주는 Controller로 이루어진 MVC패턴, 그리고 MVC에서부터 파생된 MVVM(View Model), MVW(Whatever)등의 패턴들로 이루어져 있다. 

* 여기서 공통점은 Model로, 프레임워크들의 모델은 대부분 어떻게 작동하냐면, 양방향 바인딩을 통하여 모델에 있는 값이 변하면, 뷰에서도 이를 변화시켜준다. 일단 첫 화면을 보여주고 변화에 따라 필요한 곳을 바꿔주는 것이다. 변화(MUTATION)는 상당히 복잡한 작업이다. 특정 이벤트가 발생했을 때, 모델에 변화를 일으키고, 변화를 일으킴에 따라 어떤 DOM을 가져와서 어떠한 방식으로 뷰를 업데이트 해줄 지 로직을 정해줘야 하는데, 페이스북에서는 리액트를 만들기 전에 이런 발상을 했다.

* 그냥 MUTATION 하지 않는 대신, 데이터가 바뀌면 그냥 뷰를 날리고 새로 만들어 버리면 어떨까? 하지만 DOM기반으로 작동하는 페이지를 그때그때 새로 뷰를 만들면 성능적으로 엄청난 문제가 있을 것이다.

* 그래서 virtual DOM (가상의 돔)을 사용한다.

        * 변화가 일어나면, 실제로 브라우저의 DOM에 새로운 것을 넣는게 아니라, 자바스크립트로 이루어진 가상 DOM에 한번 렌더링을 하고, 기존의 DOM과 비교를 한 다음 정말 변화가 필요한 곳에만 업데이트를 해주는 것이다.
        
        * 이 가상의 돔을 사용함으로서, 데이터가 바뀌었을 때 더이상 어떻게 업데이트를 고려하는게 아니라, 그냥 일단 바뀐 데이터로 일단 그려놓고, 비교를 한 다음에 바뀐 부부만 찾아서 바꿔주는 거다.
        
        * virtual DOM은 DOM 변화를 최소화 시켜주는 역할을 하는데, 이 횟수를 최소화 시키는 것은 성능적으로 매우 중요한 이슈이다.
        
        * vue, marko, maquette, mihiril 에서도 사용한다.

#### 리액트의 장점

1. 엄청난 생태계

    - 제이쿼리가 나왔을 때와 비슷하게 핫하다. 제이쿼리, 혹은 일반 자바스크립트로 만들어진 라이브러리들도 리액트로 포팅되어 많이 작성되고 있따, 뿐만 아니라 단순히 특정 기능 구현하기 위한 라이브러리(폼캐로절, 애니메이션, UI)가 아니라, 프로젝트의 구조와 강하게 묶여있는 라우터, 상태관리 라이브러리들로 매우 다양하게 만들어져있다.
    
2. 사용하는 곳이 많다.

    - airbnb, bbc, yahoo, ebay, walmart, facebook, cloudflare

3. 끝없는 공부

    - 계속해서 발전해나가지 때문에 끊임없이 공부를 해야한다,.


## React 프로젝트 시작하기

* Node, yarn, webpack, babel등의 도구를 설치하여 설정해주어야 한다.

* 리액트 프로젝트를 만들게 되면서, 컴포넌트를 여러가지 파일로 분리해서 저장을 할 것이고, 또 이 컴포넌트는 일반 자바스크립트가 아닌 JSX라는 문법으로 작성하게 된다.

* 여러가지 파일을 한개로 결합하기 위해서 우리는 webpack이라는 도구를 사용하고 JSX를 비롯한 새로운 자바스크립트 문법들을 사용하기 위해 Babel이라는 도구를 사용한다.


### 프로젝트 시작하기에 앞서, 필요한 설치 프로그램

#### 1.  Node.js

* webpack과 babel과 같은 도구들이 자바스크립트 런타임인 Node.js를 기반으로 만들어져서, 이 도구를 사용하기 위해서 Node.js 설치가 필요하다.

#### 2.  yarn

* 조금 개선된 버전의 npm이라고 생각하면 된다.
* 프로젝트에서 사용되는 라이브러리를 설치하고, 해당 라이브러리들의 버전 관리를 할 때 사용한다.
* yarn을 사용하는 이유는 더 나은 속도, 나은 캐싱 시스템을 사용하기 위함이다.

#### 3.  webpack 

* 웹프로젝트를 만들 때 전체적으로 파일들을 관리해주는 도구이다.
* 코드들을 의존하는 순서대로 하나 또는 여러개의 파일로 정리해준다.
* gulp와 약간 비슷한 느낌(bundle your script)
* 자바스크립트를 여러 개 사용했을때 하나의 파일로 만들어주는 것. 원한다면 규칙에 따라 나눠줄 수도 있다.
* 사스나, 레스 같은 걸 사용한다면 웹펙에 연동을 시켜 컴파일 해서 하나의 css 파일, 혹은 몇개의 css로 변환을 해줄 수 있다. 

#### 4.  babel 

* 자바스크립트 변환 도구
* 자바스크립트는 새로운 문법이 생기면서 노드나 브라우저의 자바스크립트 엔진에서 모든 문법을 지원하지 않는다. 때문에 지원하지 않는 자바스크립트 내용을 바벨에서 지원하도록 변환해주는 기능을 한다.
* 사이트 들어가보면 자세히 알 수 있다.


### React 구성

* 리액트를 사용하면 웹 애플리케이션에 사용하는 유저 인터페이스를, 재사용 가능한 컴포넌트로 분리하여 작성함으로서 프로젝트의 유지보수성을 우수하게 해준다.
* html같지만, 자바스크립트로 변환되는 것이다. 리엑트 컴포넌트를 작성할때 사용하는 문법이다.

        inport React {component} from React;
        
        -> 리액트와 그 내부의 component를 불러온다.
        -> 파일에서 JSX를 사용하려면, 반드시 React를 임포트 해야한다.
        
        import logo from './logo.svg';
        import './App.css';
        
        -> 같은 디렉토리에 있는 파일 logo.svg와 App.css파일을 불러왔다.
        -> 이렇게 임포트 하는것은 webpack을 사용하기에 가능한 작업으로, 이렇게 불러오고 나면 나중에 프로젝트를 빌드하게 됐을 때, webpack에서 파일의 확장자에 따라 다른 작업을 하게 된다.
        -> css 파일을 불러오게 되면, 나중에 프로젝트에서 사용한 프로젝트를 한 파일에 모두 결합해주는 작업을 진행하고, 자바스크립트 파일을 불러오게 되면 모든 코드들이 제대로 로딩되게끔 순서를 설정하고, 하나의 파일로 합쳐준다.
        -> 그리고 svg처럼 사전에 따로 설정되지 않은 확장자의 경우, 우선 파일로 불러온 다음에 나중에 특정 경로에 사본을 만들어 주게되고, 해당 사본의 경로를 텍스트로 받아오게 된다.

#### component 를 만드는 방법

1. class를 통해서 만들기 (class형 컴포넌트)

    - class 형태로 만들어진 component에는 반드시 render함수가 있어야 하고, 그 내부에는 JSX를 return 해주어야 한다.
     
    - 하단 export default App; : 작성한 component를 다른 곳에서 불러와서 사용할 수 있도록 내보내기를 해준다.
    
            class App extends Component {
                
                render(){
                    
                    return (
                    
                         <div className="App">
                             <header className="App-header">
                                <img src={logo} className="App-logo" alt="logo" />
                                <h1 className="App-title">Welcome to React</h1>
                                </header>
                             <p className="App-intro">
                                 To get started, edit <code>src/App.js</code> and save to reload.
                             </p>
                         </div>
                         
                    );
                }
            }
            
            export default App;
            
    - import App from './App';
    
        - 우리가 만든 컴포넌트를 불러올 때는 이렇게 import를 사용해서 불러와준다.
        
    - ReactDOM.render(<APP />, document.getElementById('root');
    
        - 브라우저 상에서 우리의 리액트 컴포넌트를 보여주기 위해서는 ReactDOM.render 함수를 사용한다.
            
        - 첫번째 parameter는 렌더링 할 결과물이고, 두번째 parameter는 컴포넌트를 어떤 DOM에 그릴지 정해준다.
            
        - id가 root 인 DOM을 찾아서 그리도록 설정되어 있고, 해당 DOM은 public/index.html에서 볼 수 있다. 해당 파일 안에 있는 id="root"를 찾아서 렌더링 해주게 되는 것이다.
        
                import React from 'react';
                import ReactDOM from 'react-dom';
                import './index.css';
                import App from './App';
                import registerServiceWorker from './registerServiceWorker';
                 
                ReactDOM.render(<App />, document.getElementById('root'));
                registerServiceWorker();
                
2. 함수를 통해 만드는 컴포넌트 (함수형 컴포넌트)

  - 딱히 기능없이, 뭔가를 받아와서 보여주기만 할 때 사용하는 컴포넌트 형식
  
  - 단순히 props만 받아와서 보여주기만 하는 컴포넌트의 경우에 작성하는 형태이다.
  
  - state와 LifeCycle이 빠져서, 초기 마운트 속도가 미세하게 빠르고, 불필요한 기능이 없어서 메모리 손실이 적다.
  
        import React, {Component} , from 'react';
        
        const MyName = ({ name }) => {
        
        //비구조화 할당이라고 부른다.
        
            return (
                <div>
                    안녕하세요! 제 이름은 {name}입니다.
                </div>
            )
        }
        
        export default MyName;
                    

 
 
### JSX 

1. 리액트 개발을 쉽게 하기 위해서, HTML과 비슷한 문법으로 작성을 하면, 이를 React.createElement를 사용하는 자바스크립트 형태로 변환시켜준다.

2. Javascript + XML을 합쳐서 탄생한 기존 자바스크립트의 확장 문법이다.
  
3. XML 형태의 코드를, 자바스크립트로 변환해야 하기 때문에, JSX를 제대로 사용하기 위해서 몇가지 규칙을 준수해야한다.

    A. input / br tag와 같이 열려있는 tag도 무조건 닫아야 한다.
     
            - <input type="text" />
            
            import React, { Component } from 'react';
            
            class App extends Component {
              render() {
                return (
                  <div>
                    <input type="text" />        
                  </div>
                );
              }
            }
            export default App;

    B. 두 개 이상의 엘리먼트는 무조건 하나의 엘리먼트로 감싸져야 한다.
     
            import React, { Component } from 'react';
            
            class App extends Component {
              render() {
                return (
                  <div>
                       <div>
                          Hello
                        </div>
                        <div>
                          Bye
                        </div>
                  </div>
                );
              }
            }
            export default App;
            
    C. 단순히 감싸기 위해 div를 사용하지 않고, Fragment를 사용할 수 있다. (이 기능은 v16.2 에 도입되었습니다.)
        
            import React, { Component, Fragment } from 'react';
            
            class App extends Component {
              render() {
                return (
                  <Fragment>
                    <div>
                      Hello
                    </div>
                    <div>
                      Bye
                    </div>
                  </Fragment>
                );
              }
            }
            export default App;
            
    D. JSX 안에 자바스크립트 값 사용하기
        
            import React, { Component } from 'react';
            
            class App extends Component {
              render() {
                const name = 'react';
                return (
                  <div>
                    hello {name}!
                  </div>
                );
              }
            }
            
            export default App;
        
            - var : scope가 함수 단위이다. es6에서 쓰지 않음
            - let, const : scope가 block단위이다. 
            - let : 선언 후  값을 바꿔야 할 때 사용, 유동적인 값
            - const : 선언 후 바꾸지 않을 때 사용, 고정적인 값
            function foo() {
              let a = 'hello';
              if (true) {
                let a = 'bye';
                console.log(a); // bye
              }
              console.log(a); // hello
            }
    
    E. 조건부 렌더링
    
    - 보통 삼항 연산자를 쓰거나 AND 연산자를 사용한다.
    - 반면 if문은 사용할 수 없다. 사용하려면 IIFE(즉시 실행 함수)을 사용해야 한다.
    
            - 삼항연산자
            
                import React, { Component } from 'react';
                
                class App extends Component {
                  render() {
                    return (
                      <div>
                        {
                          1 + 1 === 2 
                            ? (<div>맞아요!</div>)
                            : (<div>틀려요!</div>)
                        }
                      </div>
                    );
                  }
                }
                
                export default App;
        
            - AND연산자
            
                import React, { Component } from 'react';
                
                class App extends Component {
                  render() {
                    return (
                      <div>
                        {
                          1 + 1 === 2 && (<div>맞아요!</div>)
                        }
                      </div>
                    );
                  }
                }
                
                export default App;
                
            - IIFE
            
                import React, {Component} from 'react';
                
                class App extends Component {
                    render(){
                        const value = 1;
                        return (
                            <div>
                                {
                                  (function() {
                                    if (value === 1) return (<div>하나</div>);
                                    if (value === 2) return (<div>둘</div>);
                                    if (value === 3) return (<div>셋</div>);
                                  })()
                                }
                            </div>
                            );
                        }
                    }
                    export default App;
                    
            - switch 문 
                
                import React, {Component} from 'react';
                
                class App extends Component {
                    render(){
                        const value = 1;
                        return (
                            <div>
                                (() => {
                                  if (value === 1) return (<div>하나</div>);
                                  if (value === 2) return (<div>둘</div>);
                                  if (value === 3) return (<div>셋</div>);
                                })()
                            </div>
                            );
                        }
                    }
                    export default App;
                    
    -  화살표 함수
    
        - function표현에 비해 구문이 짧고 자신의 this, argument, super 또는 new.target을 바인딩 하지 않는다.
        - 항상 익명으로, 함수 표현은 메소드 함수가 아닌 곳에 가장 적합하다.
        - 구문 
        
                (param1, para2, ...., paraN) => {statements}
                (param1, para2, ...., paraN) => expression
                
                return expression;
                
                
                var materials = [
                  'Hydrogen',
                  'Helium',
                  'Lithium',
                  'Beryllium'
                ];
                
                materials.map(function(material) { 
                  return material.length; 
                }); // [8, 6, 7, 9]
                
                materials.map((material) => {
                  return material.length;
                }); // [8, 6, 7, 9]
                
                materials.map(({length}) => length); // [8, 6, 7, 9]
                
                  
                    
4. style과 className 

    A. style
    
    - 객체 형태로 넣어준다.
    
    - "-"말고 camelCase 형태로 넣어준다.
    
            import React, { Component } from 'react';
            
            class App extends Component {
            
                render(){
            
                    const style={
                    
                        backgroundColor = 'black',
                        padding : '16px',
                        color : '#ffffff',
                        fontSize : '36px'
                    };         
                      
                return (
                        <div style = {style}> 안녕하세요~ </div>;
                      );
                }
            }
            export default App;
        
    B. class 사용하기
    
    - 리액트 컴포넌트에서는 class 대신에 className을 사용한다.
    
            - App.css 파일
            
                .App{
                    background : black;
                    color : aqua;
                    font-siza : 15px;
                    padding:1rem;
                    font-weight:400;
                }
                
            - App.js
    
                import React , {Component} from 'react';
                import './App.css';
                
                class App extends Component {
                
                    render(){
                        return (
                            <div className="App">
                                리액트
                            </div>
                        );
                    }
                }

5. 주석

    A. {/*...*/} / // 
    
        import React, {Component} from 'react';
        
        class App extends Component {
        
            render() {
            
            return (
                <div>
                    {*/ 주석은 이렇게 /*}
                    <h1  
                        // 태그 사이에
                    > 리액트 </h1>
                </div>
            );
           }
        }
            
        export default App;
        
    
