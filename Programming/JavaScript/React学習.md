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

### propsとState

```javascript
import { useState } from 'react';

import { ColorfulMessage } from './components/ColorfulMessage';

  

export const App = () => {

  const [num, setNum] = useState(0);

  const onClickCountUp = () => {

    setNum((prev) => prev + 1);

    setNum((prev) => prev + 1);

  };

  return (

    <>

      <h1 style={{ color: 'red' }}>こんにちは</h1>

      <ColorfulMessage color="blue">お元気ですか？</ColorfulMessage>

      <ColorfulMessage color="green">元気です</ColorfulMessage>

      <button onClick={onClickCountUp}>カウントアップ</button>

      <p>{num}</p>

    </>

  );

};
```
