# JSX 
이전과 같은 방식(`React.createElement` 사용)으로 작성하면 코드가 복잡해지기 때문에
좀더 쉽게 작성하도록한다.

HTML문법과 똑같이 `<button>`을 다시 작성하고 `const e`를 삭제한다.
`ReactDOM.render` 부분도 `e()`를 지우고 `<LikeButton />`으로 작성한다.
```javascript
class LikeButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      liked: false,     // <-- 기본 상태
    }
  }

  render() {
    return <button type="submit" onClick={() => { this.setState({ liked: true }) }}>{this.state.liked === true ? 'Liked' : 'like'}</button>
    // JSX ( JS + XML )
  }
}
```
여기서 문제는 `React`는 HTML문법을 지원해주지 않기 때문에 `BABEL`이 필요하다.

BABEL CDN을 추가하고 `<script> type`을 작성한다.
그러면 자바스크립트 안에서 HTML문법을 사용할 수 있다.

`BABEL`이 `JSX`문법을 `React.createElement`로 변환해준다.
```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel"> </script>
```
여기서 사용하는 문법이 `JSX`이다
컨텐츠 부분에 `중괄호{ }`를 감싸주면 그 안에서 자바스크립트 코드를 사용할 수 있다.

만약 `<Likebutton />`을 4개를 쓰고싶다하면 추가한 만큼 알아서 내용이 채워진다. ==> component장점

[](./jsx_component.html)