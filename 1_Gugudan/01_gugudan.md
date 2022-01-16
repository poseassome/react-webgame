# 구구단 게임 만들기

## `<GuGuDan />` component를 생성한다.

### 구구단 게임에서 필요한 요소
- 랜덤한 숫자 2개
- 정답 입력 칸
- 정답 버튼
- 결과 출력 문구

모두 정해져있지 않고 바뀔 여지가 있는 부분이므로 state로 작성한다.
```jsx
class GuGudan extends React.Component {
  constructor(props){
    super(props);
    this.state = {
      first: Math.ceil(Math.random() * 9),
      second: Math.ceil(Math.random() * 9),
      value: '',
      result: '',
    }
  }
}
```
### `super(props)`를 사용하는 이유?
자식 클래스는 생성될 때, 부모 클래스의 생성자를 참조한다.<br/>
class component에서 부모 클래스는 React.Component를 말한다.

`super()`를 선언 전에는 `constructor()`안에서 `this`를 사용할 수 없다.<br/>
`props`를 전달하여 `props`를 초기화 해주고 생성자 내부에서 this.props를 사용하기 위해 작성한다.

## `render()` 내용 작성
```jsx
render() {
  return (
    <div>
      <div>{this.state.first} 곱하기 {this.state.second}는?</div>
        <form onSubmit={(e) => {
          e.preventDefault();
          if (parseInt(value) === this.state.first * this.state.second) {  // 정답일 경우 새로운 랜덤 숫자를 만들어내고 value를 초기화
            this.setState({
              result: '정답',
              first: Math.ceil(Math.random() * 9),
              second: Math.ceil(Math.random() * 9),
              value: '',
            })
          } else {   // 틀릴 경우 문제 유지하고 value 초기화
            this.setState({
              result: '땡',
              value: '',
            })
          }
        }}>
          <input type="number" value={this.state.value} onChange={(e) => this.setState({ value: e.target.value })} /> 
          <button>입력 !</button>
        </form >
      <div>{this.state.result}</div>
    </div >
    );
  }
}
```
jsx와 javascript를 섞어서 작성한 형태로, 이를 class의 메소드로 작성하기로 한다.<br/>
그러면 `<form onSubmit={this.onSumbit}>`, `<input onChange={this.onChange}>`로 바뀐다.

## class 메소드 작성 (onSubmit, onChange)
```jsx
onSubmit = (e) => {
  e.preventDefault();
  if (parseInt(this.state.value) === this.state.first * this.state.second) {
    this.setState({
      result: '정답',
      first: Math.ceil(Math.random() * 9),
      second: Math.ceil(Math.random() * 9),
      value: '',
    })
  } else {
    this.setState({
      result: '땡',
      value: '',
    })
  }
};

onChange = (e) => {
  this.setState({ value: e.target.value })
};
```
***

### 전체 코드
```html
<!DOCTYPE html>
<html lang="ko">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>구구단</title>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>

<body>
  <div id="root"></div>
  <script type="text/babel">
    class GuGuDan extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          first: Math.ceil(Math.random() * 9),
          second: Math.ceil(Math.random() * 9),
          value: '',
          result: '',
        }
      }

      onSubmit = (e) => {
        e.preventDefault();
        if (parseInt(this.state.value) === this.state.first * this.state.second) {
          this.setState({
            result: '정답',
            first: Math.ceil(Math.random() * 9),
            second: Math.ceil(Math.random() * 9),
            value: '',
          })
        } else {
          this.setState({
            result: '땡',
            value: '',
          })
        }
      };

      onChange = (e) => {
        this.setState({ value: e.target.value })
      };

      render() {
        return (
          <div>
            <div>{this.state.first} 곱하기 {this.state.second}는?</div>
            < form onSubmit={this.onSubmit} >
              <input type="number" value={this.state.value} onChange={this.onChange} />
              <button>입력 !</button>
            </form >
            <div>{this.state.result}</div>
          </div >
        );
      }
    }
  </script>
  <script type="text/babel">
    ReactDOM.render(<GuGuDan />, document.querySelector('#root'));
  </script>
</body>

</html>
```