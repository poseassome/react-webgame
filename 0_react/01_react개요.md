# React 사용하는 이유

1. 사용자 인터페이스 개선

    SPA(Single Page Application)<br/>
    웹 페이지를 앱처럼 동작하게 한다. (페이지 깜빡임이 없다.)

2. 데이터 처리

    데이터와 화면을 일치시킬 수 있다.

3. 유지보수 용이

    컴포넌트화하여 재사용이 가능한 콘텐츠를 생성할 수 있다.
<br/>
<br/>

# 컴포넌트 생성
html문서에서 기본적으로 `<div id="root"> </div>`가 필요하다.<br/>
이는 component들이 담길 부분이다.

우선 react를 설치하지 않고 CDN방식으로 가져오도록 한다.
```html
<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```
`react`는 `javascript`기반이므로 `<script>`안에 작성하도록 한다.

### class component 생성
```javascript
const e = React.createElement;

class LikeButton extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return e('button', { onClick: () => { console.log('clicked') }, type: 'submit' }, 'Like');
    // --> <button onclick="()) => { console.log('clicked') }" type="submit">Like</button> 이런 태그를 형성하겠다.
  }
}
```
`React.createElement`를 변수에 할당하여 component을 작성한다.
```jsx
React.createElement( component, props, ...children )
// 순서대로 'HTML 요소', 'HTML 속성', 'text'을 작성한다.
```
'HTML 속성'을 작성할 때는 camel case로 작성한다 `(onclick -> onClick)`
<br/>
<br/>

### state(상태)
component의 강점으로 state(상태)가 있다.

위 example에서 만약 `Like` 글자가 바뀐다면 `Like`가 `state`가 된다.<Br/>
즉, 바뀔 여지가 있는 부분이 `state(상태)`이다.<br/>
상태는 `this.state ={ }` 로 작성한다.

* ***react developer tools*** 설치하면 개발자도구에서 컴포넌트별로 확인할 수 있다.

바뀐 상태를 화면에 반영하려면 `render(){ }` 안에서 작성하면 된다.
```jsx
const e = React.createElement;

class LikeButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      liked: false,     // <-- 기본 상태
    }
  }

  render() {
    return e(
      'button', 
      { onClick: () => { this.setState({ liked: true }) }, type: 'submit' }, 
      this.state.liked === true ? 'Liked' : 'Like'
    );
    // 클릭을 하면 true로 바꿔줌
  }
}
```
`this.state.liked`가 `true`이면 `button`의 text를 `Liked`로 바꿔라.

여기서, class하나가 component하나라고 보면 된다.

[class로 컴포넌트 생성](./class_component.html)