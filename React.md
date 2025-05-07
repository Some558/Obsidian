### Reactでのイベントの当て方
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