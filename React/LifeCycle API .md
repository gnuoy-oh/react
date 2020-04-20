## LifeCycle API

- 컴포넌트가 브라우저에 나타날 때, 사라질 때, 업데이트 될 때, 호출되는 API이다. 

### 컴포넌트 초기생성 (Mounting)  
    
#### 1. constructor

- 컴포넌트 생성자 함수이다.

- 컴포넌트가 새로 만들어질 때마다 이 함수가 호출된다.

        constructor(props){
        
            super(props);
            
        }
        
#### 2. componentWillMount

- 컴포넌트가 화면에 나가기 직전에 호출되는 API이다.

- 주로 브라우저가 아닌 환경에서(서버사이드)도 호출하는 용도로 사용했었으나, 이 API가 더이상 필요하지 않게 됨

- UNSAFE_componentWillMount() 라는 이름으로 사용된다.

#### 3. componentDidMount

- 컴포넌트가 화면에 나타나게 됐을 때 호출된다.

- 주로 D3, masonry 처럼 DOM을 사용해야하는 외부 라이브러리를 연동하거나, 해당 컴포넌트에서 필요로하는 데이터를 요청하기 위해 axios, fetch 등을 통하여 ajax를 요청을 하거나,
DOM의 속성을 읽거나 직접 변경하는 작업을 진행한다.


### 컴포넌트 업데이트 (Updating) - 컴포넌트 props나 state가 바뀔 때

- 컴포넌트가 업데이트는 props의 변화, 그리고 state의 변화에 따라 결정된다.

- 업데이트 되기 전과 그리고 된 후에 어떤 API가 호출되는지 살펴보자 !!

#### 1. componentWillReceiveProps

- 이 API는 컴포넌트가 새로운 props를 받게 됐을 때 호출된다.

- 주로 state가 props에 따라 변해야 하는 로직을 작성한다. 

- 새로 받게될 props는 nextProps로 조회할 수 있으며, 이 때 this.props를 조회하면 업데이트 되기 전의 API이다.

- v16.3부터 deprecate되어서 UNSAFT_componentWillReceiveProps() 라는 이름으로 사용된다.

        componentWillReceiveProps(nextProps){
        
        
            }
            
#### 2. static getDerivedStateFromProps()

- 이 함수는 v16.3 이후에 만들어진 API인데, 이 API는 props로 받아온 값을 state로 동기화하는 작업을 해줘야 하는 경우에 사용된다.
        
        static getDerivedStateFromProps(nextProps, preState){
        
        
        // 여기서는 setState를 하는 것이 아니라
        // 특정 props가 바뀔 때 설정하고, 설정하고 싶은 state값을 리턴하는 형태로 사용된다.
        /*
        
            if(nextProps.value !== prevState.value){
            
                return { value : nextProps.value };
            }
        
            return null; // null을 리턴하면 따로 업데이트 할 것은 없다는 뜻    
        */
        
        }      

#### 3. shouldComponentUpdate()



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
        
        
     
         
         
                