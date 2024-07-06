## Unsplash Image API를 활용한 이미지 검색 사이트 만들기

### 프로젝트 설명

1. react-router를 활용하여 페이지 라우팅을 구현
   동일한 UI를 사용하고 특정 조건 파라미터에 부분에 따라서 이미지만 다르게 보여야 하는 페이지는 path 값에 id값을 활용

2. nav. JSON 파일을 만들어 데이터를 분리하여 코드 가독성을 높임
   Link 태그를 사용해서 nav. JSON에 정의한 패스 경로로 내비게이션이 이루어지도록 구현
   (a 태그를 사용하면 페이지 전체를 새로 렌더링하여 속도가 저하되는 문제가 발생하기 떄문에 Link 태그를 사용
   Link 태그는 브라우저의 주소만 바꿀 뿐, 페이지 자체를 새로 고치지 않는다)

2-1. 내비게이션 영역에 단어를 클릭했을 떄 해당 페이지가 라우팅 작업을 통해 단어와 일치한 이미지를 호출
변경한 데이터에 따라서 리코일 스토어가 바뀌게 했습니다.

3. 시멘틱 태그 사용하였고 CSS module 사용으로 전역적인 충돌을 방지

4. 일반 변수로 데이터를 조작했을 때는 화면이 변하지 않아 usestate를 사용해서 반복적인 UI를 그려줄 부분에 데이터를 불변성을 유지하며 배열 형태로 만들고 map 함수를 활용하여 UI를 구성

5. API 통신을 위해 axios 설치, 비동기적으로 API호출하기 위해 async await 문법을 사용

6. API에서 받아온 데이터에 타입을 정의하고 props를 통해 데이터와 고유한 key 값을 전달하고 이미지 데이터를 호출해 UI에 표시

6-1.중앙집중식 상태관리인 Recoil 통해서 공통으로 자주 사용되는 state나 API는 스토어에서 관리해서 필요할 떄 호출하는 방식을 사용하여, 유지보수와 관리에 신경 썼습니다.

7. usestate와 &&를 활용해서 true일때만 나타는 UI를 구현하며 boolean 값을 통해 관리할 수 있다는것을 배웠습니다.

8.index/components/Card 컴포넌트와 DetailDialog 컴포넌트에 API 데이터 바인딩을 활용하여 Card 컴포넌트에서 호출한 이미지를 DetailDialog에 전달하여 이미지를 클릭했을 때 동일한 이미지가 나오도록 하였고 false를 전달하여 닫기 버튼을 업데이트하였습니다.

9. map 함수를 통해 Card 컴포넌트 UI를 그리는 페이지가 마운트 되기 전에 스테이트를 호출한 에러가 발생 계속 호출할 필요가 없어서 useMemo를 활용하여 Card 컴포넌트를 최적화하여 메모리에 저장해 놓고 필요할 때마다 또는 의존성 배열이 변할때만 메모리에서 꺼내도록 사용했습니다.

10. SearchBar 컴포넌트에 useState와 Recoil을 활용해 검색 기능을 구현 - 빈값으로 검색하였을 때 atoms에 설정한 기본값이 검색 되도록 구현

- React.KeyboardEvent를 활용하여 Enter 키를 눌러도 검색되도록 구현

11. footer 컴포넌트에 페이지 네이션을 recoil과 useEffect를 활용하여 API에 토탈 페이지에 있는 데이터를 호출하여 다음 페이지로 이동했을 때 이미지가 나오도록 구현, 검색했을 때 일치하는 이미지가 나오고 첫 번째 페이지로 이동하도록 구현

12. css loader spinner에 있는 아이콘을 활용하여 API 호출할 때 상태가 로딩인 경우에만 동작하도록 구현

13. 다이얼로그 창에 북마크 버튼을 눌렀을 때 선택한 데이터를 로컬스토리지에 저장
    로컬스토리지에 저장한 데이터를 새로운 라우팅을 통해 만든 북마크 페이지에 호출하여 props 타입을 정의하고 props를 가지고 데이터 바인딩 하였고
    헤더 부분은 동일한 컴포넌트를 재사용했습니다.

### 개발환경

1.  프로젝트 환경설정(vite를 활용한 React 설치): `npm install vite@latest` <br />

2.  React 중앙집중식 상태관리 라이브러리 Recoil 설치: `npm install recoil` <br />

3.  외부 오픈 API 통신을 위한 라이브러리 Axios 설치: `npm install axios` <br />

4.  CSS 스타일링을 위한 SASS/SCSS 설치: `npm install -D sass` <br />

5.  React Router 설치: `npm install react-router-dom localforage match-sorter sort-by` <br />

6.  TypeScript에서 Node.js 모듈을 쓸 수 있는 환경 구축 : `npm i @types/node` <br />

7.  React Toast Popup 모듈 설치 : `npm install react-simple-toasts` <br />
