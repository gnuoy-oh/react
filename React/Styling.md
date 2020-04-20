## 다양한 방식의 리액트 컴포넌트 스타일링

### Styled-component

#### Styled-component 설치 와 코드 

- npm install --save styled-components

            import React, {Component, Fragment} from 'react';
            imort styled, {creagteGlobalStyle, css, keyframes} from 'styled-components';

            class App extends Component{
                render(){
                    return (
                        <Fragment>
                            <button>Hello</button>
                            <button danger>Hello</button>
                        </Fragment>
                    )
                }
            }

            const Button = styled.button`
                    border-radius: 50px;
                    padding: 5px;
                    min-width: 120px;
                    color: white;
                    font-weight: 600;
                    -webkit-appearance: none;
                    cursor: pointer;
                    &:active,
                    &:focus {
                    outline: none;
                    }
                    background-color: ${props => (props.danger ? 'red' : 'purple')}

                    // props로 style을 변경하기

                    ${props => {
                        if(props.danger) {
                            return css `animatio: ${rotation} 2s linear infinite`;
                        }
                    }}
            `

            const rotation = kerframes`
                from{
                    opacity:1;
                }
                to{
                    opacity:0;
                }
            `

    - Button component에 rotationTime을 props로 css를 변경

                <Button danger rotationTime={5}></Button>

                const Button = styled.button`
                    ---생략---
                    ${props => {
                        if (props.danger) {
                            return css `animation: ${rotation} ${props.rotationTime}s linear infinite`
                        }
                    }}
                `

#### Styled-component 사용법

- styled 객체 안에 styled-component를 import 해주고, Button 변수에 styled.button 방식으로 html button 태그를 css와 함께 담아준다.

- 마지막 background-color > props에 체크해서, red 혹은 purple로 지정할 수 있다.

1. withComonent 메소드는 새로운 stylecomponent를 생성하고, 다른 태그에 적용 시킨다.

    - 예를 들어 button 태그의 stylecomponent를 a 태그에 적용시키고 싶다면,

                const Anchor = Button.withCompontne('a');

    - css를 추가하고 싶다면, styled 메소드를 이용한다.

                const Anchor = styled(Button.withComponent('a'))`
                    text-decoration: none;
                `
                <Anchor href="http://naver.com">Go to Naver</Anchor>

2. keyframes 

    - animation을 위한 keyframes을 생성하는 메소드

    - @keyframes란?

        - @keyframes 는 css 문법중 하나로 애니메이션이 만들어지는 부분.

        - @keyframes 를 타임라인 안의 하나의 스테이지(구간).

        - @keyframes 안에서 우리는 스테이지들을 정의하고 각 구간마다 다른 스타일을 적용 시킬 수 있다.

                    @keyframes tutsFade애니메이션이름 {
                        from{
                            opacity:1;
                        }
                        to{
                            opacity:0;
                        }
                    }

                    .element{
                        animation: tutsFade 4s 1s infinite linear alternate;
                    }

3. tag의 속성을 변경해보기

    - attrs를 이용해서 태그의 속성을 변경할 수 있다.

                const InputCheckbox = styled.input.attrs({
                    type: 'checkbox',
                    checked: true,
                })`
                    border-radius: 5px;
                    color:red;
                `

    - mixin (스타일 시트 전체에서 재사용 할 CSS 선언 그룹을 정의하는 기능 )

        - styled-component의 css 메소드를 이용해서 style을 정의하고 변수로 추가해줬다.

                    const awesomeCard = css`
                        box-shadow: 0 4px 6px blue, 0 1px 3px blue;
                        background-color: white;
                        border-radius: 10px;
                        padding: 20px;
                    `;

                    const InputCheckbox = styled.input.attrs({
                        type: 'checkbox',
                        checked: true,
                    })`
                        border-radius: 5px;
                        color: red;
                        ${awsomeCard} // <== 추가 
                    `;

    - ThemeProvider를 이용해서 React Child component까지 제공된 테마를 적용하는 방법

    1. themes.js를 생성

                const theme = {
                    mainColor: 'red',
                    dangerColor: 'blue',
                    successColor: 'gray',
                }

                export default theme;
    
    2. App.js에서 ThemeProvider와 theme을 import 한 뒤, 컴포넌트 최 상단에 ThemeProvider 컴포넌트에 theme을 props로 넣어준다.

                import React, {createGlobalStyle, ThemeProvider} from 'styled-component';
                import themes from './themes';

                const Card = styled.div'
                    background-color: white;
                ';

                const Button = styled.button`
                    border-radius: 30px;
                    padding: 25px 15px;
                    background-color: ${props => props.theme.dangerColor} // <== props.theme의 값을 설정할 수 있음
                `;

                class App extends Component {
                    render(){
                        return (
                            <ThemeProvider theme={themes}>    // <== props
                                <React.Fragment>
                                <GlobalStyle />
                                <Container>
                                    <Form />
                                </Container>
                                </React.Fragment>
                            </ThemeProvider>
                        )
                    }
                }

                const Form = () => (
                    <Card>
                        <Button>Hello</Button>
                    </Card>
                )



                
                




- 참고 Link

    - https://www.styled-components.com/docs/basics

    - https://javaexpert.tistory.com/1020

    - https://velog.io/@taewo/%EB%A6%AC%EC%95%A1%ED%8A%B8-Styled-Components-76jsolbaf8

    - https://www.daleseo.com/react-styled-components/