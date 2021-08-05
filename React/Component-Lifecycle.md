#React Component Lifecycle
<img src="https://user-images.githubusercontent.com/33210124/128347774-15d5ccc1-eb56-4ee3-9c7b-8874a3143573.png">
component가 생기면 constructor가 먼저 실행된다(하지만 이때의 component는 준비가 다 된 상태가 아님)
render가 호출되고 세팅이 완료 된 다음이 준비가 된 상태임.
componentDidMount는 render가 되고, 리액트가 DOM을 업데이트 하고 난 다음 사용할 준비가 됐다고 알려준다 -> 제일 많이 씀
반대로 component가 필요가 없어질 때는 언마운팅된다고 하며 이때 componentWillUnmount가 호출되고 component가 삭제된다.
render가 일어날때는 새로운 props이 들어왔을때, setState()로 스테이트가 변경됐을 때 자동으로 일어난다. 
render가 정상적으로 끝나게 되면 componentDidUpdate가 호출된다.
