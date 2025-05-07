### Reactでのイベントの当て方
```javaScript
export const App = () => {

  const onClickButton = () => alert();

  return (

    <>

      <h1>こんにちは</h1>

      <p>お元気ですか</p>

      {console.log('hoge')}

      <button onClick={onClickButton}>ボタン</button>

    </>

  );

};
```


### Reactでのスタイルの当て方
```javaScript
export const App = () => {

  const onClickButton = () => alert();

  const contentStyle = {

    color: 'blue',

    fontSize: '18px',

    margin: 10,

  };

  return (

    <>

      <h1 style={{ color: 'red' }}>こんにちは</h1>

      <p style={contentStyle}>お元気ですか</p>

      <button onClick={onClickButton}>ボタン</button>

    </>

  );

};
```