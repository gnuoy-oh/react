## React

### LINK

- 스터디 : https://ko.reactjs.org/docs/getting-started.html

- 실제 연습 Repository : https://github.com/ohmy0418/REACT_DOCS_2019.git

### 용어 정리

#### 1. Componenets

- 컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있다.

- 개념적으로 컴포넌트는 JS 함수와 유사하다. 

- props라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환한다. 

- 가장 간단한 React 컴포넌트는 React 엘리먼트를 반환하는 일반 Javascript 함수이다.

      function Welcome(props){
        return <h1>Hello, {props.name)</h1>
      }

- 컴포넌트는 ES6 class로도 작성할 수 있다.

      class Welcome extends React.Component{
        render(){
          return <h1>Hello, {}</h1>
        }
      }

1. 함수 컴포넌트와 클래스 컴포넌트

  - 컴포넌트를 정의하는 가장 간단한 방법은 JavaScript 함수를 작성하는 것이다.

        function Welcome(props){
          return <h1>Hello, {props.name}</h1>;
        }

  - 이 함수는 데이터를 가진 하나의 "props"(props는 속성을 나타내는 데이터) 객체 인자를 받은 후 React 엘리먼트를 반환하므로, 유효한 React 컴포넌트디아. 이러한 컴포넌트는 JS 함수이기 때문에 말 그대로 "함수 컴포넌트" 라고 한다.

  - 또한 ES6 class를 사용하여 컴포넌트를 정의할 수 있다.

      class Welcome extends React.Component{
        render(){
          return <h1>Hello, {this.props.name}</h1>;
        }
      }

  - 두 가지 유형의 컴포넌트는 동일하다.

2. 컴포넌트 렌더링

  - 이전까지는 React 엘리먼트를 DOM태그로 나타냈다.

        const elemenet = <div />;

  - React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있다.
      
        const element = <Welcome name="Sara">

  - React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면, JSX 어트리뷰트를 해당 컴포넌트에 단일 객체로 전달한다. 이 객체를 "props"라고 한다.

      - 예시

            function Welcome(props){
              return <h1>Hellom {props.name}</h1>;
            }

            const element = <Welcome name="Sara" />;

            ReactDOM.render(
              element,
              document.getElementById('root')
            );

      - 설명
      1. <Welcome name = "Sara" /> 엘리먼트로 ReactDOM.render()를 호출한다.

      2. React는 {name : 'Sara'}를 props로 하여, Welcome 컴포넌트르 호출한다.

      3. Welcome 컴포넌트르 결과적으로 <h1>Hello, Sara</h2> 엘리먼트를 반환한다.

      4. ReactDOM은 <h1>Hello, Sara</h1> 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트 한다.

      - 주의 : 컴포넌트의 이름은 항상 대문자로 시작한다.

        - 소문자로 시자하면 DOM 태그로 처리한다. 

3. 컴포넌트 합성 

  - 컴포넌트를 자신의 출력에 다른 컴포넌트를 참조할 수 있다.

  - 모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있음을 의미한다.

  - React 앱에서는 버튼, 폼, 다이얼로그, 화면 등의 모든 것들이 흔히 컴포넌트로 표현된다.

  - Welcome을 여러 번 렌더링하는 App 컴포넌트를 만들 수 있다.

        function Welcome(props){
          return <h1>Hello, {props.name}</h1>; 
        }

        function App(){
          return(
            <div>
              <Welcome name = "Sara" />
              <Welcome name = "Mongu" />
              <Welcome name = "Cheeze" />
            </div>
          );
        }

        ReactDOM.render(
          <App />,
          document.elementById('root)
        )

  - 일반적으로 새 React 앱은 최상위에 단일 App 컴포넌트를 가지고 있다. 하지만 기존 앱에 React를 통합하는 경우에는 button과 같이 작은 컴포넌트부터 시작해서 뷰 계층의 상단으로 올라가면서 점진적으로 작업해야 할 수 있다.

4. 컴포넌트 추출 - 컴포넌트를 여러 개의 작은 컴포넌트로 나누기

      - 예시

            function Comment(props){
              return (
                <div className = "Comment">
                  <div className = "UserInfo>
                    <img className="Avatar" 
                      src={props.author.avatarUrl}
                      alt{props.author.name}
                    /> 
                    <div className="UserInfo-name">
                      {props.author.name}
                    </div>
                  </div>
                  <div className="Comment-text">
                    {props.text}
                  </div>
                  <div className="Comment-date">
                    {formatDate(props.date)}
                  </div>
                </div>
              );
            }

      - 이 컴포넌트는 author(객체), text(문자열), date(날짜) 를 props로 받은 후, 소셜 미디어 웹 사이트의 코멘트를 나타낸다. 

      - 이 컴포넌트는 구성요소들이 모두 중첩 구조로 이루어져 있어서 변경하기 어려울 수 있으며, 각 구성요소를 개별적으로 재사용 하기도 힘들다. 
      
      - 이 컴포넌트에서 몇 가지 컴포넌트를 추출해보자.

      1. Avatar 추출

              function Avatar(props){
                return(
                  <img className="Avatar"
                    src={props.user.avatarUrl}
                    alt={props.user.name}
                  />
                );
              }
      - Avatar는 자신이 Comment 내에서 렌다링 된다는 것을 알 필요가 없다. 따라서 props의 이름을 author에서 더울 일반화 된 user으로 변경했다.

      - props의 이름은 사용될 context가 아닌, 컴포넌트 자체의 관점에서 짓는 것을 권장한다.

            ->  Avatar 추출 후 Comment 
                  function Comment(props){
                    return (
                      <div className="Comment">
                        <div className="UserInfo">
                          <Avatar user={props.author} />
                          <div className="UserInfo-name">
                            {props.author.name}
                          </div>
                        </div>
                        <div className="Comment-text">
                          {prpps.text}
                        </div>
                        <div className="Comment-date">
                          {formatDate(props.date)}
                        </div>
                      </div>
                    );
                  }

      2. Avatar 옆에 사용자의 이름을 렌더링하는 UserInfo 컴포넌트를 추출하기

              function UserInfo(props){
                return(
                  <div className="UserInfo">
                    <Avatar user={props.user}/>
                    <div className="UserInfo-name">
                      {props.user.name}
                    </div>
                  </div>
                );
              }

              -> UserInfo 추출 후 Comments
              function Comment(props){
                return(
                  <div className="Comment">
                    <UserInfo name={props.author} />
                    <div className="Comment-text">
                      {props.text}
                    </div>
                    <div className="Comment-date">
                      {formatDate(props.date)}
                    </div>
                  </div>
                );
              }

  - 처음에는 컴포넌트를 추출하는 작업이 어려울 수 있다.

  - 하지만 재사용 가능한 컴포넌트를 만들어 놓는 것은 더 큰 앱에서 작업할 때 두각을 나타낸다.

  - UI 일부가 여러 번 사용되거나 (button,panel,avatar), UI 일부가 자체적으로 복잡한(App,FeedStory,Comment) 경우에는 재사용 가능한 컴포넌트로 만드는 것이 좋다.

#### 2. Props

1. props는 읽기 전용이다.

  - 함수 컴포넌트나, 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안된다. 

        function sum(a,b){
          return a+b;
        }

        - 이런 함수들은 순수 함수라고 호칭한다. 
        - 입력 값을 바꾸려 하지 않고, 항상 동일한 입력값에 대해 동일한 결과를 반환한다.

        function withdraw(account,amont){
          account.total -= amount;
        }

        - 이런 함수들은 입력값을 변경하기 때문에 순수 함수가 아니다.
  
  - React는 한가지 엄격한 규칙이 있다.

### 모든 React 컴포넌트는 자신의 props를 다룰 때, 반드시 순수 함수처럼 동작해야 한다.

- 물론 애플리케이션 UI는 동적이며 시간에 따라 변한다. React 컴포넌트는 state를 통해 위 규칙을 위반하지 않고, 사용자 액션, 네트워크 응답 및 다른 요소에 대한 응답으로 시간에 따라 자신의 출력값을 변경할 수 있다. 

#### 3. state

- Clock이 스스로 타이머를 설정하고 매초 스스로 업데이트 하도록 만들기

      class Clock extends React.Component{
        constructor(props){
          super(props);
          this.state = {date:new Date()};
        }

        render(){
          return(
            <div>
              <h1>Hello, World</h1>
              <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
          )
        }
      }
      ReactDOM.render(
        <Clock />,
        document.getElementById('root')
      )

### JSX 소개

const element = <h1>Hello, World! </h1>;

- JSX는 React 엘리먼트(element)를 생성한다. 

- 리액트에서는 이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등 렌더링 로직이 본질적으로 다른 UI 로직과 연결된다는 사실을 받아들인다.

- 리액트는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 "컴포넌트"라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리한다. 이후 섹션에서 다시 컴포넌트로 돌아오겠지만, JS에 마크업을 넣는 것!

- 리액트는 JSX 사용이 필수가 아니지만, 대부분의 사람은 JS코드 안에서 UI 관련 작업을 할 때, 시각적으로 더 도움이 된다고 생각을 하고 있다. 또한 리액트가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해준다.

1. JSX 표현식 포함하기

  - name 이라는 변수를 선언한 후, 중괄호로 감싸 JSX 안에 사용하기

        const name = 'josh perez';
        const element = <h1>hellom {name}</h1>

        ReactDOM.render(
          elemenent,
          document.getElementById('root');
        )

  - JSX의 중괄호 안에는 유효한 모든 JS 표현식을 넣을 수 있다.

    - 예를 들어, 2 + 2 , user.firstName, formatName(user) 등..

  - JS 호출 결과인 formatName(user)을 <h1> 엘리먼트에 포함하기

        function formatName(user){
          return user.firstName + ' ' + user.lastName;
        }

        const user = {
          firstName : 'harper',
          lastName : 'perez'
        }

        const element = (
          <h1>
            hello, {formatName(user)}!
          </h1>
        );

        ReactDOM.render(
          element,
          document.getElemenetById('root');
        )

2. JSX도 표현식이다

  - 컴파일이 끝나면, JSX 표현식이 정규 JS 함수 호출이 되고, JS 객체로 인식된다.

  - 즉, JSX를 if 구문 및 for loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있다.

        function getGreeting(user){
          is(user){
            return <h1> hello, {formatName(user)}!<h1>;
          } 
          return <h1> hello, Stranger.<h1>;
        }

3. JSX 속성 정의

  - 속성에 따옴표를 이용해 문자열 리터럴을 정의할 수 있다.

       const elemenet = <div targetIndex="0"></div>;

  - 중괄호를 사용하여 attribute에 JS 표현식을 삽입할 수도 있다.

        const element = <img src={user.avataUrl} />;  

  - attribute에 JS 표현식을 삽입할 때 중괄호 주변에 따옴표를 입력하지 않는다. 따옴표 (문자열 값에 사용) 혹은 중괄호(표현식에 사용) 중 하나만 사용하고, 동일한 attribute에 두 가지를 동시에 사용하면 안된다.

  - JSX는 HTML보다는 JS에 가깝기 때문에, React DOM 은 HTML 어트리뷰트 이름 대신, camelCase 프로퍼티 명명 규칙을 사용한다. 

4. JSX 자식 정의

  - 태그가 비어있다면 XML처럼 /> 를 이용해 바로 닫아주어야 한다.

      const elemenet = <img src={user.avataUrl} />;

  - JSX 태그는 자식을 포함할 수 있다.

      const elemenet = (
          <div>
            <h1>HEllo!</h1>
            <h2>Good to see you here.</h2>
          </div>
      );

5. JSX는 주입 공격을 방지한다.

  - JSX에 사용자 입력을 삽입하는 것은 안전하다.

      const title = response.potentiallyMaliciousInput;
      // 이것은 안전합니다.
      const element = <h1>{title}</h1>;

  - 기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 excape하므로, 애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않는다. 모든 항목은 렌더링 되기 전에, 문자열로 반환된다. 이런 특성으로 인해 XSS(cross-site-scripting) 공격을 방지할 수 있다.

6. JSX는 객체를 표현한다.

  - babel은 JSX 를 React.createElement() 호출로 컴파일 한다.

        //다음 두 예시는 동일하다.
        const element=(
          <h1 className = "greeting">
            Hello, world!
          </h1>
        )

        const element = React.createElement(
          'h1'
          {className:'greeting'}
          'Hello, world!'
        )

  - React.createElement()는 버그가 없는 코드를 작성하는 데 도움이 되도록 몇 가지 검사를 수행하며, 기본적으로 다음과 같은 객체를 생성한다.

        const element = {
          type : 'h1',
          props : {
            className : 'greeting',
            children : 'Hello, world!'
          }
        };

  - 이러한 객체를 React 엘리먼트라고 하며, 이를 화면에 표시하려는 항목에 대한 설명이라고 생각할 수 있다. React는 이러한 객체를 읽은 후 DOM을 구성하고 최신으로 유지하는 데 이러한 객체를 사용한다.

### Element 렌더링

- 엘리먼트는 React 앱의 가장 작은 단위이다.

- 엘리먼트는 화면에 표시할 내용을 기술한다.

      const element = <h1>Hello, world</h1>;

    - 브라우저 DOM 엘리먼트와 달리, React 엘리먼트는 일반 객체 (plain object)이며, 쉽게 생성할 수 있다. React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트 한다. 

- 컴포넌트화 혼동할 수 있다. 엘리먼트는 컴포넌트의 "구성 요소" 이다.

1. DOM에 엘리먼트 렌더링 하기

  - HTML 파일 어딘가에 <div>가 있다고 가정해보자.

        <div id="root"><div>

  - 이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에, 이것을 "루트(root)"DOM 노드 라고 부른다.

  - React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있다. React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM 노드가 있을 수 있다.

  - React 엘리먼트를 루트 DOM 노드에 렌더링 하려면, 둘 다 ReactDOM.render()로 전달하면 된다.

        const elemenet = <h1>Hello, world!</h1>
        ReactDOM.render(element, document.getElemenetById('root));

2. 렌더링 된 엘리먼트 업데이트하기

  - React 엘리먼트는 불변객체이다. 엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없다. 엘리먼트는 영화에서 하나의 프레임과 같이 특정 시점의 UI를 보여준다.

  - UI를 업데이트하는 유일한 방법은, 새로운 엘리먼트를 생성하고 이를 ReactDOM.render()로 전달하는 것이다.

        // setInterval() 콜백을 이용해, 초마다 ReactDOM.render()를 호출한다.

        // html 
        <div id="root"></div>

        //JS
        function tick(){
          const element=(
            <div>
              <h1>Hello, world!</h1>
              <h2>It is {new Date().toLocaleTimeString()}.</h2>
            </div>
          );
          ReactDOM.render(elemenet, document.getElementById('root'));
        }

        setInterval(tick, 1000);

3. 변경된 부분만 업데이트하기

  - React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고, DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트 한다.

          // setInterval() 콜백을 이용해, 초마다 ReactDOM.render()를 호출한다.
          
          // html 
          <div id="root"></div>

          //JS
          function tick(){
            const element=(
              <div>
                <h1>Hello, world!</h1>
                <h2>It is {new Date().toLocaleTimeString()}.</h2>
              </div>
            );
            ReactDOM.render(elemenet, document.getElementById('root'));
          }

          setInterval(tick, 1000);

  - 매 초 전체 UI를 다시 그리도록 엘리먼트를 만들었지만, React DOM 은 내용이 변경된 텍스트 노드만 업데이트 한다.

4. function Component 에서 class Component로 변환하기 

  1. React.Component 를 확장하는 동일한 ES6 class를 생성한다.

  2. render() 라고 불리는 빈 메서드를 추가한다.

  3. 함수의 내용을 render() 메서드 안으로 옮긴다.

  4. render() 내용 안에 있는 props를 this.props로 변경한다.

  5. 남아있는 빈 함수 선언을 삭제한다.

        * function Component

        function Clock(props) {
            return (
              <div>
                <h1>Hello, world!</h1>
                <h2>It is {props.date.toLocaleTimeString()}.</h2>
              </div>
            );
          }

          function tick() {
            ReactDOM.render(
              <Clock date={new Date()} />,
              document.getElementById('root')
            );
          }

          setInterval(tick, 1000);

        * class Component

        class Clock extends React.Component{
          render(){
            return (
              <div>
                <h1>Hello, World!</h1>
                <h2>It is {this.props.date.toLocalString()}.</h2>
              </div>

            )
          }
        }

  - Clock은 더이상 함수가 아닌 class로 정의된다.

  - render 메서드는 업데이트가 발생할 때마다 호출되지만, 같은 DOM노드로 <Clock />을 렌더링하는 경우, Clock 클래스의 단일 인스턴스만 사용된다. 이것은 로컬 state와 생명주기 메스드와 같은 부가적인 기능을 사용할 수 있게 해준다.

5. Class Comonent에 로컬 state 추가하기

  - 세 단계에걸쳐서 date를 state로 이동하기

  1. render() 메서드 안에 있는 this.props.date를 this.state.date로 변경하기

        class Clock extends React.Component{
          render(){
            return (
              <div>
                <h1>Hello, World</h1>
                <h2>It is {this.state.date.toLocaleTimingString()}</h2>
              </div>
            );
          }
        }

  2. 초기 this.state를 지정하는 class constructor 를 추가한다.

  - Constructor : class로 생성된 객체를 생성하고 초기화하기 위한 특수한 메소드, 부모 클래스의 constructor를 호출하기위해 super 키워드를 사용

        class Clock extends React.Component{
          constructor(props){
            super(props);
            this.state= {date:new Date()};
          }
          
          reder(){
            return(
              <div>
                <h1>Hello, World</h1>
                <h2>It is {this.state.date.toLocaleTimingString()}</h2>
              </div>
            );
          }
        }
    
    - class Component는 항상 props로 기본 constructor를 호출해야 한다.

  3. <Clock /> 요소에서 date props을 삭제한다.

        ReactDOM.render(
          <Clock />,
          document.getElementById('root')
        )

  * 결과

        class Clock extends React.Comonent{
          constructor(props){
            super(props)
            this.state = {date : new Date()}
          }

          render(){
            return(
              <div>
                <h1>Hello, World</h1>
                <h2>It is {this.state.date.toLocaleTimingString()}</h2>
              </div>
            )
          }
        }

        ReactDOM.render(
          <Clock />
          document.getElementById('root')
        )

6. 생명주기 메서드를 클래스에 추가하기

- 많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요하다.

- Clock이 처음 DOM에 렌더링 될 때마다 타이머를 설정하려고 한다. ==> mounting === componentDidMount

  - componentDidMount : 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행된다. 이 순간이 타이머를 설정하기 좋은 순간이다.

- Clock에 의해 생성된 DOM이 삭제될 때마다 타이머를 해제하려고 한다.==> unmount === componentWillUnmount

- 이런 메서드들은 "생명주기 메서드"라고 한다.

- 컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트 되거나, 언마운트 될 때 일부 코드를 작동할 수 있다.

      class Clock extends React.Component{
        constructor(props){
          super(props)
          this.state = {date : new Date()}
        }

        componentDidMount(){
          <!-- 타이머 ID를 제대로 저장하는지 주의해서 볼 것  -->
          this.timerID= setInterval(
            ()=>this.tick(), 1000
          )
        }

        componentWillUnmount(){
          clearInterval(this.timerID);
        }

        <!-- Clock 컴포넌트가 매 초 작동하도록 하는 tick 메서드 구현 -->
        tick(){
          <!-- 컴포넌트 로컬 state를 업데이트 하기 위해 this.setState()를 사용한다. -->
          this.setState({
            date : new Date()
          })
        }


        render{
          return(
              <div>
                <h1>Hello, World</h1>
                <h2>It is {this.state.date.toLocaleTimingString()}</h2>
              </div> 
          )
        }
      }

      ReactDOM.render(
        <Clock />
        document.getElementById('root');
      )

- 설명

  1. <Clock />가 ReatDOM.render()로 전달되었을 때, React는 Clock 컴포넌트의 constructor를 호출한다.Clock이 현재 시각을 표시해야 하기때문에 현재 시각이 표함된 객체로 this.state를 초기화 한다. 나중에 이 state를 업데이트 할 것이다.

  2. React는 Clock 컴포넌트의 render() 메서드를 호출한다. 이를 통해 React는 화면에 표시되어야 할 내용을 알게된다. 그 다음 React Clock의 렌더링 출력값을 일치시키기 위해 DOM을 업데이트 한다.

  3. Clock 출력값이 DOM에 삽입되면, React는 componentDidMount() 메서드를 호출한다. 그 안에서 Clock 컴포넌트는 매 초 컴포넌트의 tick() 를 호출하기 위한 타이머를 설정하도록 브라우저에 요청한다.

  4. 매초 브라우저가 tick() 메서드를 호출한다. 그 안에서 Clock 컴포넌트는 setState()에 현재 시각을 포함하는 객체를 

----------------------------------정리 해야함












### Hook

- HOOK을 이용해서 class를 작성할 필요없이, 상태 값과 여러 react 기능을 사용할 수 있다.

  - 선택적 사용, 기존의 코드를 다시 작성할 필요 없이, 일부의 컴포넌트들 안에서 Hook을 사용할 수 있다.

  - class가 코드의 재사용성과 코드 구성을 좀 더 어렵게 만들 뿐 아니라, react를 배우는데 큰 진입 장벽이 될 수 있다. 이런 다양한문제를 해결하기 위해 hook는 class 없이 react 기능들을 사용하는 방법을 알려준다. 

  1. State Hook

  - 버튼을 클릭하면 증가하는 간단한 카운터 예시

        import React, {useState} from 'react';

        funtion Example(){
          //count 라는 새 상태 변수를 선언한다.
          const [count, setCount] = useState[0];

          return(
            <div>
              <p>You clicke {count} times</p>
              <button onClick={() => setCount(count + 1)}>
                Click me
              </button>
            </div>
          );
        }

        - 여기서 useState 가 Hook이다. Hook(useState)를 호출해 function component안에 state 를 추가했다. 이 state는 컴포넌트가 다시 렌더링 되어도 그대로 유지될 것이다. 

        - useState는 현재의 state 값과 이 값을 업데이트하는 함수를 쌍으로 제공한다. 

        - 이 함수를 이벤트 핸들러나, 다른 곳으로 호출할 수 있다. 이 것을 class 의 this.setState와 거의 유사하지만, 이전 state와 새로운 state를 합지지 않는다는 차이점이 있다. 

        - useState는 인자로 초기 state 값을 하나 받고, 카운터는 0부터 시작하기 때문에 위 예시에서는 초기 값으로 0을 넣어준 것이다. this.state와 달리 setState Hook의 state는 객체일 필요가없다. 이 초깃값은 첫 번째 렌더링에만 딱 한번 사용된다.

  - 여러 state 변수 선언하기

    - 하나의 컴포넌트 내에서 state hook을 여러개 사용할 수도 있다.

          function ExampleWithManyStates(){
            //상태 변수를 여러개 선언
            const [age, setAge] = useState(42);
            const [fruits, setFruit] = useState('banana');
            const [todos, setTodos] =  useState({text: 'Learn Hooks'})
          }

    - 배열 구조 분해(destructuring)문법은 useState로 호출된 state 변수들을 다른 변수명으로 할당할 수 있게 해준다. 이 변수명은 useState API와관련이없다.대신 react를 매번 렌더링할 때 useState가 사용된순서대로 실행할 것이다.

         - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EB%B0%B0%EC%97%B4_%EA%B5%AC%EC%A1%B0_%EB%B6%84%ED%95%B4

  - Hook은 ? 

    - hook은 함수 컴포넌트 react state와 생명주기 기능(lifecycle features)을 연동(hook into)할 수 있게 해주는 함수이다. hook은 class 안에서 동작하지 않고, 대신 class 없이 react를 사용할 수 있게 해주는 것이다.

    - react는 useState와 같이 내장 hook을 몇 가지 제공한다. 

  - Effect Hook

    - react컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 할 수 있다. 이런 모든 모든 동작을 (side effect=effects)라고 한다. 왜냐하면 이것은 다른 컴포넌트에 영향을 줄 수도 있고,렌더링 과정에서 구현할 수 없는 작업이기 때문이다. 

    - effect hook, 즉 useEffect는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해준다. 
    
    - react class의 componentDidMount / componentDidUpdate / componentWillUnmount와 같은 목적으로 제공되지만, 하나의 API로 통합된 것이다. 

    - 예시 react가 DOM을 업데이트 한 뒤에 문서의 타이틀을 바꾸는 컴포넌트

          import React, {useState, useEffect} from 'react';

          function Example(){
            const [count, setCount] = useState[0];

            //componentDidMount, componentDidUpdate와 비슷하다.
            useEffect( () => {
              //브라우저 API를 이용해 문서의 타이틀을 업데이트 한다.

              document.title= `you clicked ${count} times`;

            });

            return (
              <div>
                <p>You clicke {count} times</p>
                <button onClick={() => setCount(count + 1)}>
                  Click me
                </button>
              </div>
            )
          }
    
    - useEffect를 사용하면, react는 DOM을 바꾼 뒤에, "effect" 함수를 실행할 것이다. Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있다. 기본적으로 react는 매 렌더링 후에 effects를 실행한다. 

- Hook 사용 규칙

  1. 최상위 (at the top level) 에서만 Hook을 호출해야 한다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하면 안된다.

  2. React 함수 컴포넌트 내에서만 Hook을 호출해야 한다. 일반 JS 함수에선 Hook을 호출해서는 안된다.

- 나만의 Hook 만들기!

  - 개발을 하다보면 가끔 상태관련 로직을 컴포넌트 간에 재사용하고 싶은 경우가 생긴다. 이 문제를 해결하기 위한 방법 두 가지는 higher-order components와 render props 이다.

  - custom hook는 컴포넌트 트리에 새 컴포넌트를 추가하지 않고도 가능하게 해준다.

        import React, {useState, useEffect} from 'react';

        function useFriendStatus(friendID){
          const [isOnline, setIsOnline] = useState(null);

          function handleStatusChange(status){
            setIsOnline(status.isOnline);
          }

          useEffect(() => {
            chatAPI.subscribeToFriendStatus(friendID, handleStatusChange);

            return () =>{
               ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
            }
          })
        }

        return isOnline

    - 각 컴포넌트의 state는 완전히 독립적이다. Hook은 state 그 자체가 아니라, 상태 관련 로직을 재사용하는 방법이다.

    - 실제로 각각의 Hook 호출은 완전히 독립된 state를 가진다.그래서 심지어 한 컴포넌트 안에같은 custom hook를 두 번 쓸 수 있다.

    - Custom Hook은 기능이라기보다는 컨벤션(convention)에 가깝습니다. 이름이 ”use“로 시작하고, 안에서 다른 Hook을 호출한다면 그 함수를 custom Hook이라고 부를 수 있다. useSomething이라는 네이밍 컨벤션은 linter 플러그인이 Hook을 인식하고 버그를 찾을 수 있게 해준다.

#### Using the State Hook

- Hook 예시

      import React,{useState} from 'react';

      function Example(){
        // 새로운 state 변수를 선언하고, 이를 count라고 부른다. 
        const [count,setCount] = useState[0];

        return (
          <div>
            <p>You clicke {count} times</p>
            <button onClick={() => setCount(count + 1)}>
              Click me
            </button>
          </div>
        )
      }

- Hook과 같은 기능을 하는 class 예시

  - 아래 코드는 {count : 0} 이며, 사용자가 this.setState()를 호출하는 버튼을 클릭했을 때 state.count를 증가시킨다. 

        class Example extends React.Component{
          constructor(props){
            super(props);
            this.state = {
              count : 0
            };
          }

          render(){
            return (
              <div>
                <p>You Clicked {this.state.count} times</p>
                <button onClick = {() => this.setState({ count : this.state.count + 1})>
                  Click Me
                </button>
              </div>
              
            )
          }
        }

- Hook과 함수 컴포넌트

  - React function component 두 가지 

        //case 1
        const Example = (props) =>{
          //여기서 Hook 사용
          return <div />;
        }

        //case 2
        function Example(props){
          //여기서 Hook 사용
          return <div />;
        }

- 함수 컴포넌트를 State가 없는 컴포넌트라고 알고 있었을 테지만, Hook은 react state를 함수 안에서 사용할 수 있게 해준다!

- Hook은 class 안에서 동작하지 않는다~

#### Hook

- useState의 경우! state 함수 컴포넌트 안에서 사용할 수 있게 해준다. (다른 목적의 Hook들 존재)

- function component를 사용하던 중 state를 추가하고 싶을 때, class component로 바꾸지 않고 사용하기 위함

1. state 변수 선언하기

  - class의 경우, constructor 안에서 this.state를{count:0} 으로 설정함으로써 count를 0으로 초기화 했다.

        class Example extends React.Component{
          constructor(props){
            super(props);
            this.state= {
              count : 0;
            }
          }
        }

  - function component는 this를 가질 수 없기 때문에 this.state를 할당하거나 읽을 수 없다. 대신, useState Hook를 직접 컴포넌트에 호출할 수 있다.

        import React, {useState} from 'react';

        function Example(){
          // 새로운 state 변수를 선언하고, 이것을 count라 부르겠습니다.
          const [count, setCount] = useState(0);
        }

    - count 라고 부르는 state 변수를 선언하고, 0 으로 초기화 한다. React는 해당 변수를 리렌더링 할 때 기억하고, 가장 최근에 갱신된 값을 제공한다. 

    - count 변수의 값을 갱신하려면, setCount를 호출하면 된다.

    - useState를 호출하는 것은 무엇을 하는 것?

      - state 변수를 선언할 수 있다. 위에 예시의 변수는 count라고 부르지만, banana 처럼 아무 이름으로 지어도 된다.

      - useState는 class component의 this.state가 제공하는 기능과 똑같다. 

      - 일반적으로 일반 변수 함수가 끝날 때 사라지지만, state 변수는 react에 의해 사라지지 않는다.

    - useState의 인자로 무엇을 넘겨주어야 하나?

      - useState() Hook의 인자로 넘겨주는 값은 state의 초깃값이다. 함수 컴포넌트의 state는 클래스 컴포넌트와 달리 객체가 필요없고, 숫자와 문자 타입을 가질 수 있다.

      - 위의 예시에는 사용자가 버튼을 얼마나 많이 클릭했는지 알기 원하므로 0을 해당 state의 초깃값으로 선언했다.

      - 2개의 다른 변수를 저장하기를 원한다면, useState()를 두 번 호출한다.

    - useState 는 무엇을 반환하나?

      - state변수. 해당 변수를 갱신할 수 있는 함수 이 두 가지 쌍을 반환한다.

      - const [count, setCount] = useState() 라고 쓰는 이유이다.

      - 클래스 컴포넌트의 this.state.count 와 this.setState와 유사하다.

2. state 가져오기

  - class component : count를 보여주기 위해 this.state.count를 사용한다.

  - function component : {count}를 직접 사용

3. state 갱신하기

  - class component : count를 갱신하기 위해, this.setState() 호출한다.

  - function component : setCount와 count 변수를 가지고 있으므로, this 호출하지 않아도 된다.

4. 요약

        // useState Hook 을 React 에서 가져온다.
        import React, {useState} from 'react'; 

        function Example(){
          // useState Hook 을 이용하면, state 변수와 해당 state를 갱신할 수 있는 함수가 만들어 진다.
          // 또한, useState의 인자의 값으로 0을 넘겨주면 count 값을 0으로 초기화할 수 있습니다.
          const [count, setCount] = useState(0);

          return (
            <div>
              <p>You Clicked {this.state.count} times</p>
              // 사용자가 버튼 클릭을 하면 setConut 함수를 호출하여 state 변수를 갱신합니다.
              // React는 새로운 count 변수를 Example 컴포넌트에 넘기며 해당 컴포넌트를 리렌더링합니다.
              <button onClick = {() => this.setState({ count : this.state.count + 1})>
                Click Me
              </button>
            </div>
          )
        }

### Router?

- URL 값에 따른 뷰(View)를 보여주는 역할

- 사용자가 요청한 URL의 서브 디렉토리에 따라서 결과물을 렌더링 해준다.

- 처음부터 웹앱에서 사용 할 모든 컴포넌트를 먼저 불러와두고, 페이지를 이동할 때마다 그때그때 페이지를 처음부터 로딩하지 않고, 필요한 컴포넌트만 다시 렌더링 한다.

- 즉, header와 같은 부분처럼 변동이 없는 부분들은 유지되어 있는 것이다.

- 참고 : https://velopert.com/1173

  - https://niceman.tistory.com/59

1. react Router 설치

  - npm을 통해서 react-router를 설치

        npm install --save react-router

  - index.js의 상단에 코드 추가

        import {Router, Route, browserHistory, IndexRoute} from 'react-router';

  - App.js의 상단에 코드 추가

        import {Link} from 'react-router'

### useCotext

- context 객체(React.createContext에서 반환된 값)을 받아 그 context의 현재 값을 반환한다.

- context의 현재 값은 트리 안에서 이 Hook을 호출하는 컴포넌트에 가장 가까이 있는 <Mycontext.Provider>의 value prop에 의해 결정된다.

- 컴포넌트에서 가장 가까운 <MyContext.Provider>가 갱신되면 이 Hook은 MyContext provider에게 전달된 가장 최신의 context value를 제공하여 렌더러를 트리거 한다.

- useContext로 전달한 인자는 context 객체 그 자체이어야 함을 잊지 마세요.

      맞는 사용: useContext(MyContext)
      틀린 사용: useContext(MyContext.Consumer)
      틀린 사용: useContext(MyContext.Provider)
          
- useContext를 호출한 컴포넌트는 context 값이 변경되면 항상 리렌더링 될 것입니다. 만약 컴포넌트를 리렌더링 하는 것에 비용이 많이 든다면, 메모이제이션을 사용하여 최적화할 수 있습니다.

### Context?

- context는 React 컴포넌트 안에서 전역적(global)이라고 볼 수있는 데이터를 공유할 수 있도록 고안된 방법이다. 

- 예) 데이터로는 현재 로그인한 유저, 테마, 선호하는 언어 등이 있다. 

- 아래 예시) 코드의 버튼 컴포넌트를 꾸미기 위해 테마 props를 명시적으로 넘겨주고 있다.

      class App extends React.Component{
        render(){
          return <Toolbar theme="dark" />;
        }
      }

      function Toolbar(props){
        //Toolbar 컴포넌트는 불필요한 테마props를 받아서 themeButton에 전달해야 한다.
        //앱 안의 모든 버튼이 테마를 알아야 한다면, 이정보를 일일이 넘기는 과정은 매우 곤혹스러울 것,

        return (
          <div>
            <ThemeButton theme={props.theme} />
          </div>
        );
      }

      class ThemeButton extends React.Component{
        render(){
          return <Button theme="this.props.theme" />;
        }
      }

- context를 사용하면, 중간에 있는 엘리먼트 들에게 props를 넘겨주지 않아도 된다.

      // context를 사용하면, 모든 컴포넌트를 일일이 통하지 않고, 원하는 값을 컴포넌트 트리 깊숙한 곳까지 보낼 수 있다. 
      // light 를 기본값으로 하는 테마 context를 만들어 보자
      const ThemeContext = React.createContext('light');

      class App extends React.Component{
        render(){
          //Provider를 이용해, 하위 트리에 테마 값을 보내준다.
          //아무리 깊숙히 있어도, 모든 컴포넌트가 이 값을 읽을 수 있다.
          //아래 예시에서는 dark를 현재 테마 값으로 보내고 있다.
          return (
            <ThemeContext.Provider value = "dark" >
              <Toolbar />
            </ThemeContext.Provider>
          )
        }
      }

      // 중간에 있는 컴포넌트가 일일이 테마를 넘겨 줄 필요가없다.
      function Toolbar(props){
        return(
          <div>
            <ThemeButton />
          </div>
        )
      }

      class ThemeButton extends React.Component{
        //현재 선택된 테마 값을 읽기 위해 contextType을 지정한다.
        //React는 가장 가까이에 있는 테마 Provider를 찾아, 그 값을 사용할 것이다.
        // 이 예시에서 선택된 테마는 dark 이다.
        static contextType = ThemeContext;
        render(){
          return (
            <Button theme={this.context} />;
          )
        }
      }

#### context의 사용하기 전에고려할 것      

- 주된 용도 : 다양한 레벨에 네스팅된 많은 컴포넌트에게 데이터를 전달하는 것이다.

- 여러 레벨에 걸쳐 props 넘기는걸 대체하는 데에 context보다 컴포넌트 합성이 더 간단한 해결책일 수도 있다.

#### API

1. React.createContext 

       const MyContext = React.createContext(defaultValue);

  - context 객체를 만든다.

  - context 객체를 구독하고 있는 컴포넌트를 렌더링 할 때, React는 트리 상위에서 가장 가까이 있ㄴㄴ 짝이 맞는 Provider로부터 현재 값을 읽ㄴㄴ다.

  - defaultValue 매게변수는 트리 안에서 적절한 Provider를 찾이 못했을 때에만 쓰이는 값이다.

  - 컴포넌트를 독립적으로 테스트할 때 유용한 값이다.

  - Provider를 통해 undefined 값을 내보낸다고 해도, 구독 컴포넌트들이 defaultValue를 읽지 않는다는 점을 유의한다.

2. Context.Provider

        <MyContext.Provider value={/* 어떤 값 */}>

  - Context 오브젝트에 포함된 React 컴포넌트인 Provider는 context를 구독하는 컴포넌트들에게 context의 변화를알리는 역할을 한다.

  - Provider는 value prop을 받아서, 이 값을 하위에 있는 컴포넌트에게 전달한다.

  - 값을 전달받을 수 있는 컴포넌트의 숭 제한은 없다.

  - Provider 하위에 또 다른 Provider를 배치하는 것도 가능하며, 이 경우 하위 Provider 값이 우선시 된다.

  - Provider 하위에서 context를 구독하는 모든 컴포넌트는 Provider의 Value prop가 바뀔 때마다 다시 렌더링 된다.

  - 이러한 전파는 shouldComponentUpdate의 영향을 받지 않으므로, 중간에 컴포넌트가 업데이트를 중지한다고 해도 트리 끝에 있는 컴포넌트까지 전달된다.

  - context 값의 바뀌었는지 여부는 Object.is와 동일한 알고리즘을 사용해 이전 값과 새로운 값을 비교해 측정됩니다.

3. class.contextType

        class Myclass extends React.Component{
          componentDidMount(){
            let value = this.context;
               /* MyContext의 값을 이용한 코드 */
          }
          componentDidMount(){
            let value = this.context;
               /* MyContext의 값을 이용한 코드 */
          }
          componentWillUnmount(){
            let value = this.context;
               /* MyContext의 값을 이용한 코드 */
          }
          render(){
            let value = this.context;
               /* MyContext의 값을 이용한 코드 */
          }
        }
        Myclass.contextType=Mycontext;

  - React.CreateContext()으로 생성한 Context 객체를 원하는 클래스의 contextType 프로퍼티로 지정할 수 있다. 

  - 그러면 그 클래스 안에서, this.context를 이용해, 해당 Context의 가장 가까운 Provider를 찾아, 그 값을 읽을 수 있게 된다. 

  - 이 값은 render를 포함한 모든 컴포넌트가 생명주기 매서드에서 사용할 수 있다. 

  - 주의

    - 이 API를 사용하면 하나의 context만 구독할 수 있습니다. 여러 context를 구독하기 위해서는 여러 context 구독하기를 참조하세요.

          class Myclass extende React.Component{
            static contextType = MyContext;
            render(){
              let value = this.context;
              /* context 값을 이용한 렌더링 */
            }
          }

4. Context.Consumer

        <MyContext.Consumer>
          {value => /* context 값을 이용한 렌더링 */}
        </MyContext.Consumer>

  - context 변화를 구독하는 React 컴포넌트이다. 

  - 함수 컴포넌트 안에서 context를 읽기 위해서 쓸 수있다.

  - Context.Consumer의 자식은 함수여야합니다. 이 함수는 context의 현재값을 받고 React 노드를 반환합니다. 

  - 이 함수가 받는 value 매개변수 값은 해당 context의 Provider 중 상위 트리에서 가장 가까운 Provider의 value prop과 동일합니다.

  - 상위에 Provider가 없다면 value 매개변수 값은 createContext()에 보냈던 defaultValue와 동일할 것입니다.

