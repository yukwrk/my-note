---
title: "React"
tags: ""
---
## Reactとは

-   Facebook社が提供する「UIのためのライブラリ」
-   コンポーネントの定義・管理やそのレンダリング（描画）戦略の提供を行う
-   Reactでは通常はHTMLタグを模した「JSX」と呼ばれる記法を用いてコンポーネントを定義
-   JSXはbabelによってReact.createElementなどに変換される

## component

##### クラスコンポーネント

-   classキーワードを用いてコンポーネントを定義
-   状態（state）を持つことができ、描画内容を柔軟に変化させることができる

```js
    class Panel extends React.Component {
      render() { return <div>Hi</div> }

      // コンポーネントを再レンダリングすべきか否かを制御できる
      shouldComponentUpdate(nextProp, nextState) {
        return false;
      }
    }
```

##### 関数コンポーネント

-   状態（state）を持たず、一切の制御ができない
-   渡された値に従って特定の固定要素を描画するだけの、単なるプレースホルダ

## props

-   コンポーネントの属性の事
-   親のコンポーネントから子のコンポーネントに属性を渡したい時使う
-   あるデータの属性について参照できるもの
-   数値文字列配列関数など様々なものが使用できる
-   基本{}で渡す
-   デフォルトpropsを設定できる

```js
        const App = () => {
          return(
            <div>
              <User name={"Taro"}/> #propsの定義
            </div>
          )
        }

        const User = (props) => {  #定義されたpropsを渡して参照している
        return <div>Hi! I am {props.name}</div>;
        }
```

-   変数に配列としてpropsを定義しmapメソッドを使って取り出す処理例

```js
        const App = () => {

          const profiles = [
            {name: "Taro", age: 10},
            {name: "Hanako", age: 5}
          ]

          return(
            <div>
              {
                profiles.map((profile, index) => {
                  return <User name={profile.name} age={profile.age} />
                })
              }
            </div>
          )
        }

        const User = (props) => {
        return <div>Hi! I am {props.name} {props.age} years old</div>;
        }
```

## prop-types(型チェック）

```js
    User.propTypes = {
      name: PropTypes.string,
      age: PropTypes.number.isRequired
    }
```

## state

-   コンポーネントの内部の状態のこと
-   コンポーネントの内部でのみ使用される
-   propsは変更不可な値なのに対してstateは変更可な値

```js
    import React, { Component } from "react";

    const App = () => (<Counter></Counter>);

    class Counter extends Component {
    // constructorメソッドでインスタンスに対して初期化処理をしている
      constructor(props){
        super(props)
    // 初期値を設定している
        this.state = { count: 1}
      }

      handlePlusButton = () => {
    // 状態を変えるときはsetStateを使う
        this.setState({ count: this.state.count + 1})
      }

      handleMinusButton = () => {
        this.setState({ count: this.state.count - 1})
      }

      render(){
      return (
        <React.Fragment>
          <div>count: {this.state.count}</div>
          {/* 参照するときはthis.state.fooの形 */}
          <button onClick={this.handlePlusButton}>+1</button>
          <button onClick={this.handleMinusButton}>-1</button>
        </React.Fragment>
        )
      }
    }

    export default App;

```

## Hooks
