## Props 와 state

- 이 둘은 데이터를 다룰 때 사용되는 개념이다. 

### Props  
    
* 부모 컴포넌트가 자식 컴포넌트에게 데이터를 가져다 줄 때 사용한다.

    - <Child value = "value" />

* 자식 컴포넌트에서는 props를 받아오기만 하면 되고, 받아온 props를 직접 수정할 수는 없다. 

#### 새로운 컴포넌트 만들기!

- src 디렉토리에서 MyName.js 이라는 컴포넌트를 만들기

        import React, {Component} from 'react';
        
        
        class MyName extends Component {
        
            render(){
            
                return (
                    
                    <div>
                        안녕하세요~ 제 이름은 <b>{this.props.name}</b> 입니다.
                    </div>                    
                );                
            }
        }
        
        export default MyName;
        
        - 자신이 받아온 props 값은 this. 키워드를 통해서 조회할 수 있다.
        - 지금 name이라는 props를 보여주도록 했으니, 이 컴포넌트를 사용하자!
        
- App.js

        import React, {Component} from 'react';
        import MyName from './MyName';
        
        class App extends Component {
        
            render() {
            
                return (
                    <MyName name = "리액트"/>
                )
            }
        } 
        
        export default App;
        
        - import를 통하여 컴포넌트를 불러오고, 렌더링 해보았다.
        - 이렇게 컴포넌트를 만들고 나면, 일반 태그를 작성하듯이 작성해주면 된다.
        - 그리고 props 값음 name = "리액트" 이런식으로 태그의 속성을 설정해주는 것 처럼 작성한다.
        



#### defaultProps

- 가끔씩은 실수로 Props를 잊을 수 있다.

- 혹은 특정 상황에 props를 일부로 비워야 할 경우도 있다.

- 이러한 경우에, props의 기본 값을 설정해줄 수 있다. 

- 자식 입장에서는 읽기 전용이다.

        import React, {Component} from 'react';
        
        class MyName extends Component {
            
            static defaultProps = {
            
                name : "기본이름";
                
            }
               
            render() {
            
                return (
                
                    <div>
                        안녕하세요! 제 이름은 <b>{this.props.name}</b>입니다.
                    </div>
                )
            }
        }
        
        export default MyName;
        
- 이렇게 하면 만약 <MyName /> 이렇게 name 값을 생략해버리면, "기본이름"이 나타나게 된다.

- 참고로 defaultProps 는 다음과 같은 형태로도 설정할 수 있다.

- 함수형 컴포넌트에서 default Props를 설정할땐 위 방식으로 하면 된다.

        import React, {Component} from 'react';
        
        class MyName extends Component {
            
            render(){
                return (
                <div>
                안녕하세요! 제 이름은 <b>{this.props.name}</b>입니다.
                </div>
                );
            }        
        }
        
        MyName.defaultProps = {
        
            name : '기본이름'
            
        };
        
        export default MyName;
        

### state  
    
* 동적인 데이터를 다룰 땐 state를 사용한다. 

* 컴포넌트의 state 를 정의할 때는 class fields 문법을 사용해서 정의한다.

* 무조건 객체 형태로 작성해야 한다. state = { } 

* 컴포넌트 자기 자신이 가지고 있는 값 

* 내부에서 변경할 수 있고, 변경할 때는 언제나 setState라는 함수를 사용한다.

#### 새로운 컴포넌트 만들기!

- src 디렉토리에서 Counter.js라는 파일을 생성하기

        import React, {Component} from 'react';
        
        class Counter extends Component {
       
            state = {
                number : 0
            }
            
            //메소드를 만들어준다.
            
            handleIncreast = ( ) => {
            
                this.setState({
                    
                    number : this.state.number + 1                    
               
                });
                
            }
            
            handleDecreast = ( ) => {
            
                this.setState({
                    
                    number : this.state.number - 1                    
               
                });
                
            }
        
        
            render(){
            
                return (
                    
                    <div>
                    
                        <h1>카운터 세기</h1>
                        
                        <div>값 : {this.state.number} </div>
                        
                        <button onClick = {this.handleIncrease}> + </button>
                        
                        <button onClick = {this.handleDecrease}> - </button>
                        
                    </div>
                                        
                )
            
            }
       
        }
        
- 화살표 함수 사용 없이 state 사용하기

        import React , { Component } from 'react';
        
        class Counter extends Component {
        
            constructor(props){
            
                super(props);
                
                this.handleIncrease = this.handleIncrease.bind(this);
                this.handleDecrease = this.handleDecrease.bind(this);
        
            ]
            
              handleIncrease() {
                this.setState({
                  number: this.state.number + 1
                });
              }
            
              handleDecrease() {
                this.setState({
                  number: this.state.number - 1
                });
              }
              
            render(){
                return (
                  <div>
                    <h1>카운터</h1>
                    <div>값: {this.state.number}</div>
                    <button onClick={this.handleIncrease}>+</button>
                    <button onClick={this.handleDecrease}>-</button>
                  </div>
                );
            }
        }
        
        
#### 이 컴포넌트를 App에 불러와서 렌더링 하기

- 렌더링

        import React, {Component} from 'react';
        
        import Counter from './Counter';
        
        class App extends Component{
        
            render(){
                
                return(
                
                    <Counter />
                    
                )
            }
        }
        
        export default App;
        
#### state 정의

- 위에 코드를 살펴보자.

- 우선, 컴포넌트의 state를 정의할 때는 class fields 문법을 사용해서 정의한다.

- class fields 를 사용하는건 편의를 위한것이다. 확실히 constructor에 넣은 것 보다는 편하다.(위 코드가) 

- 만약 class fields를 사용하지 않으면, 다음과 같이 사용한다.

        import React, {Component} from 'react';
        
        
           class Counter extends Component {
        
            constructor(props){
                
                // 하단 supur(props); 호출한 이유 : 컴포넌트를 만들게 되면서, component를 상속했으며, 이렇게 constructor를 작성하게 되면 기존의 
                class 생성자를 덮어 쓰게 된다. 그렇기에 리액트 컴포넌트가 지니고 있던 생성자를 super를 통해 미리 실행하고,
                그 다음에 우리가 할 작업 (state)를 설정해주는 것이다. 
                
                super(props);
                    
                this.state = {
                
                    number : 0
                    
                }
            }
        
            render (){
                
            }
        }        
      

### setState  
    
* 메소드에 들어있는 this.setState 

* state에 있는 값을 바꾸기 위해서는, this.setState를 무조건 거쳐야 한다. 리액트에서는 이 함수가 호출되면 컴포넌트가 리렌더링 되도록 설계되어있다.
 
* setState 는, 객체로 전달되는 값만 업데이트를 해준다.

        - 예시 
        
        state = {
        
            number : 0 ,
            
            foo : "bar"
        }

        - this.setState({ number : 1 }) 을 하면, foo는 그대로 남고, number값만 업데이트 된다.
        
        - setState는 객체의 깊숙한 곳까지 확인하지 못한다.
        
        - 예시 2
        
         state = {
            
            number : 0,
            
            foo : {
            
                bar : 0,
                
                foobar : 1
                    
            }
            
         }
         
         - 아래와 같이 명령을 해도 foobar 값이 업데이트 되지 않고, 기존의 foo 객체가 아예 바뀌어 버린다
         
         this.setState ({
            foo : {
                foobar : 2 
            }
         })
         
         // {
            number : 0,
            foo: {
                foobar : 2
                 }   
             }
         //
         
         - 그러므로 대신 하단처럼 바꿔야 한다.
         - ...은 전개 연산자로, 기존 객체안에 있는 내용을 해당 위치에다가 풀어준다는 의미이다. 
         - 그 다음에, 우리가 설정하고 싶은 값을 또 넣어주면 해당 값을 덮어쓰게 된다.
         
         this.setState ({
         
            number : 0,
            
            foo : {
            
                ...this.state.foo,
         
                foobar : 2
                
            }
        }
               
#### setState에 객체 대신 함수를 전달하기
   
   - setState를 사용하여 값을 업데이트 하게 될 때, 기존의 값으 참고하여 값을 업데이트 하게 될 때, 조금 더 나은 문법으로 할 수 있다.
    
   
   - 기존의 작성하던 방식
   
           //메소드를 만들어준다.
           
           handleIncreast = ( ) => {
           
               this.setState({
                   
                   number : this.state.number + 1                    
              
               });
               
           }
            

        
   - 큰 문제는 아니지만, 굳이 또 this.state.를 조회해야 하는데, 아래와 같이 문법을 작성할 수도 있다.
   
         this.setSetate(
         
            (state) => ({
                
                number : state.number
              
            })
         )
        
   - setSetate에 updater 함수를 만들어서 전달해주었다. 조금 더 나아가면 아래와 같이 작성할 수도 있다.
   
   - (state)  가 ({ number })가 되었다. 이것은 비구조화할당이라고 하는 문법이다.
   
         this.setState ({
            
            ({number}) = ({
            
                number : number + 1
            
            })
         })
         
         - 이렇게도 작성이 가능
         
         const { number } = this.state;
         
         - 즉
         
         conset { number } = this.state; 
         
         this.setState({
         
            number : umber + 1
            
         })
         

### 이벤트 설정
    
* render 함수에서 이벤트 설정을 한 부분을 확인해보자.

        render(){
        
            return(
            
                <div>
                
                    <h1> 카운터 </h1>
                    
                    <div>값 : {this.state.number}/div>
                    
                    <button onClick = {this.handleIncrease}>+</button>
                    
                    <button onClick = {this.handleDecrease}>-</button>
                </div>
                
            )
       
        }

* 버튼이 클릭되면 준비한 함수가 각각 호출되도록 설정해주었다. 기존의 자스로 비슷한 작업이 있다.

* html에서 onClick 속성에 클릭되면 실행 할 자바스크립트를 문자열 형태로 넣어준다.

    <button onclick = "alert('hello');">Click Me </button>
    
* 반면 리액트에서 이벤트 함수를 설정할 때 html과 다음과 같은 사항이 다르다.

    <button onClick = {this.handleIncrease}>+</button>
    
    - 이벤트 이름을 설정할 때 camelCase로 설정해야 한다.
        
        - onclick 은 onClick
        - onmousedown은 onMouseDown
        - onchange는 onChange
        
    - 이벤트에 전달해주는 값은 함수 여야 한다. 만약 onClick = {this.handleIncrease()} 와 같이 함수 실행을 하면,
        렌더링을 할 때 마다 해당 함수가 호출이 되므로, 렌더링->함수호출->setState->렌더링->함수호출->setState->... 된다.
        
        
     
         
         
                