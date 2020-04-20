## Atomic Design 에 대해

### Atomic?

- 디자인 시스템을 만드는 하나의 방법론으로서, 5개의 구분된 단계가 있다.

    1. Atoms (원자)
    
    2. Molecules (분자)
    
    3. Organisms (유기)
    
    4. Templates
    
    5. Pages

### React 디렉토리 구조 

-  Atomic Design

    - Pages > system(Components) > basic(Components) 로 이어지는 3단 구조

![Large example image](../images/atom_base.png "Large example image")

#### Atom

- 웹 인터페이스에 적용되며, 원자는 품의 텍스트 레이블, 인풋빌드 혹은 버튼과 같은 HTML elemenet 이다.

- span, button 같은 기본 html element 개념으로 생각하면 된다.

- 컬러 팔레트, 폰트, 애니메이션과 같은 인터페이스에서 보이지 않는 추상적인 요소가 포함되기도 한다. 

#### molecules

![Medium example image](../images/atom_components.png "Medium example image")

- 예를 들어, 폼의 텍스트 레이블 / 인풋 필드 혹은 버튼들과 같이 각 개별 요소들 자체만으로는 그다지 유용하지 않지만, 폼(form)으로 구성되어 결합하면 실제로 뭔가 할 수 있다.

- Atom을 적당히모아, 사용하기 쉽게 구조화 했거나, html 태그를 래핑한 리액트 컴포넌트 단위이다. 이런 컴포넌트들을 components 폴더에 모아둔다.

- 재사용될 일이 많기 때문에, 최대한 시스템과 독립적으로 행동할 수 있도록, 액션이나 스토어와 관련없이 독립적으로 동작해야 한다.

- 다른 프로젝트에 가져다 써도 문제가 없을 정도로 독립성을 유지한다.

- 이 레벨에 존재하는 대부분의 컴포넌트의 propTypes 에는 onChange 또는 onClick 함수가 포함된다.

#### organism

![Medium example image](../images/atom_post.png "Medium example image")

- 비교적 복잡하며, 인터페이스에서 구분된 영역을 형성하는 서로 결합되어 있는 분자 그룹이다.

- 최종 인터페이스가 어떻게 보이는지 시작하는 단계로, 서로 비슷하거나 아니면 서로 상이한 분자 유형으로 구성될 수 있는데, 마스터헤드(핵심) 유기체는 로고, 메인 네비게이션, 검색, 소셜 미디어 채널 리스트와
 같은 다양한 컴포넌트로 구성될 수 있다.  

- 시스템과 연관되어, 도메인의 개념을 나타내는 컴포넌트 (서버에서 받아온 json 응답의 형식에 의존적 이거나, 해당 컴포넌트에 엑션이 포함된다거나, ajax 요청을 통해서만 초기화 될 수 있다거나, ajax 요청을 보내야 하거나, 팝업을 띄우는 등)들은 system으로 묶인다.

- 이 것들이 atomic design 관점에서 보자면, organism에 해당되는 컴포넌트 들이다. 

- 물론, 이 레벨에서 작성된 대부분의 컴포넌트가 molecules 레벨의 컴포넌트를 사용하고 있다. 반대 방향의 의존성은 없다.

- 또한 organism 을 모은 templates 대신, 페이지 조각? 페이지와 이런 페이지를 영역별로 조각조각 나눈 part-of-page 컴포넌트들이 page에 페이지를 구성하는 컴포넌트와 함께 들어있다. 

#### Templates

- 페이지를 구성하기 위해 서로 엮인 Organism 그룹으로 구성되며, 이 부분에서 디자인을 확인하고, 레이아웃이 실제로 구동하는지 볼 수 있다.

- 템플릿은 매우 구체적이며 상대적으로 추상적인 atoms / molecules/ organis 에 대한 맥락을 제공한다.

#### Page

![Medium example image](../images/atom_post_list.png "Medium example image")

- 페이지는 템플릿의 특정 인스턴스다. 사용자가 보는 디자인을 정확하고 구체적으로 구현한다. 

- 직접 Store/Actions 와 데이터를 주고받아, 페이지 조각 컴포넌트에게 전달 받은 데이터를 내려주는 형태를 띄고있다. 

- 각 페이지마다 액션과 스토어를 따로 관리하고 있다.

