# コーディング規約

## コンポーネントファイル

* 拡張子には.tsxを使用する。

    ```
    SampleComponent.tsx
    ```

* パスカルケースを使用する。

    ```
    SampleComponent.tsx
    ```

* ドメインと機能を表したものにする。

    ```
    UserName.tsx
    ```

* ファイル名とコンポーネント名を一致させる

## ディレクトリ名

* キャメルケース

    ```
    userName
    ```

## ファイル毎のルール

* componentファイル
  * [JSDoc](https://www.typescriptlang.org/ja/docs/handbook/jsdoc-supported-types.html#param%E3%81%A8returns:~:text=Try-,%40param,%40returns,-%40param%E3%81%AF%40type)の記載を行う

    ```
    /**
    * @param {string}  p1 - 文字列パラメータ
    * @param {string} [p2] - 任意のパラメータ(JSDoc構文).
    * @param {string} [p3="test"] - デフォルト値を持つ任意のパラメータ
    * @return {string} 結果
    */
    ```

  * 拡張子には.tsxを使用する。

        ```
        SampleComponent.tsx
        ```

  * パスカルケースを使用する。

        ```
        FirstLetterUpper.tsx
        ```

  * ドメインや機能に基づく命名にする。

        ```
        getAllBookName.ts → ドメイン：本 / 機能：名前一覧取得
        ```

  * ファイル名とコンポーネント名を一致させる。

        ```
        コンポーネント名:DogList ファイル名：DogsList.tsx
        ```

* storeファイル
  * [JSDoc](https://www.typescriptlang.org/ja/docs/handbook/jsdoc-supported-types.html#param%E3%81%A8returns:~:text=Try-,%40param,%40returns,-%40param%E3%81%AF%40type)の記載を行う

    ```
    /**
    * @param {string}  p1 - 文字列パラメータ
    * @param {string} [p2] - 任意のパラメータ(JSDoc構文).
    * @param {string} [p3="test"] - デフォルト値を持つ任意のパラメータ
    * @return {string} 結果
    */
    ```

  * 拡張子には.tsを使用する。

        ```
        dogsStore.ts
        ```

  * キャメルケースを使用する。

        ```
        sampleStore.ts
        ```

  * ファイル名を ストアするもの+Store.ts にする。

        ```
        userNameStore.ts
        ```

  * ドメインや機能に基づく命名にする。

        ```
        bookListStore.ts → ドメイン：本 / 機能：名前　　 に関するストアファイル
        ```

* hooksファイル
  * [JSDoc](https://www.typescriptlang.org/ja/docs/handbook/jsdoc-supported-types.html#param%E3%81%A8returns:~:text=Try-,%40param,%40returns,-%40param%E3%81%AF%40type)の記載を行う

    ```
    /**
    * @param {string}  p1 - 文字列パラメータ
    * @param {string} [p2] - 任意のパラメータ(JSDoc構文).
    * @param {string} [p3="test"] - デフォルト値を持つ任意のパラメータ
    * @return {string} 結果
    */
    ```

  * useから始め、対象になっている特定の機能を特定できるファイル名にする。

        ```
        useUser.ts
        ```

  * ドメインや機能に基づく命名にする。

        ```
        useAllUserInfo.ts → ドメイン：ユーザー / 機能：全員の情報を取得
        ```

## 定数

* 定数は全て大文字のスネークケースで定義する

    ```
    const PRODUCTION_NUMBER =123;
    ```

## 変数

* 変数はキャメルケースで定義する。

    ```
    const userName = 'サンプル 太郎'
    ```

* 配列やオブジェクトなど複数のデータをもっている変数は複数形で定義する。

    ```
    const users = [
       { id: 1 , name: 'taro' },
       { id: 2 , name: 'hanako' },
      ]
    ```

* 宣言時はconstのみ使用する

    ```
    const userName = 'サンプル 太郎'
    ```

* 配列の要素は　~List ではなく、複数形の ~s で表現する

    ```
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name} ({user.age} years old)
        </li>
      ))}
    </ul>
    ```

* 必ずany以外の型定義を行う

    ```
    const name: string = 'サンプル 太郎'
    ```

## 関数

* 関数名
  * ドメインや機能に基づく命名にする。

        ```
        const getUserAge = () => return 25;
        ```

  * キャメルケースで宣言する。

        ```
        const getUserAge = () => return 25;
        ```

* カスタムフックの命名
  * use で始める キャメルケースを使用する。

        ```
        useUser, useProductData
        ```

* イベントハンドラの命名
  * handle で始める キャメルケースを使用する。

        ```
        handleClick, handleSubmit
        ```

* 一般的なユーティリティ関数の命名
  * キャメルケース を使用する。

        ```
        fetchData, calculateTotal
        ```

* 戻り値、引数の型定義を行う

    ```
    interface User {
      name: string;
      age: number;
    }

    const getUserAge = (user: User): number => {
      return user.age;
    }

    // 使用例
    const user: User = { name: 'サンプル 太郎', age: 28 };
    console.log(getUserAge(user)); // 28
    ```

## roop文

* 配列操作時は基本的に map や filter などの配列用関数を使用する
* ループカウンタを使用しない場合は拡張 for 文を使用する

```
ダメな例
const name:string[] = {"Suzuki", "Katou", "Yamada"};

for (i = 0; i < name.length; i++){
  console.log(name[i]);
}
```

```
良い例
const name:string[] = {"Suzuki", "Katou", "Yamada"};

for (name:string){
  console.log(name);
}
```

## 条件分岐

* else がない場合は即 return する

```
const isAdult = (age: number): boolean => {
  if (age < 18) return false;
  return true;
}
```

* 厳密等価演算子(===)を使用する

```
if(barakichiSmileScore === 100){
    console.log('いい笑顔のようです^ ^')
}
```

* 条件として、!value などは行わない
  * nullを想定しているのか、falseを想定しているのかわからないため(その他、0, "", undefined, NaN なども通ってしまう)

    ```
    if(value === false){
        console.log('ニコニコ笑顔')
    }
    ```

## 型宣言に関して

* typeを用いて宣言する

```
type Member = {
  nickName: string;
  isHuman: boolean;
  level: number;
};
```

## importの記載序列

下記の順番かつアルファベット昇順で記載する。

1. 外部ライブラリ（Node Modulesからのインポート）
    * Reactやその他の外部ライブラリ（例：react, react-dom, lodashなど）。
2. プロジェクト内のモジュール（内部ライブラリやユーティリティ）
    * プロジェクト内で作成したファイルやモジュール（例：components, utils, servicesなど）。
3. スタイルやCSSファイル
    * スタイルシートやCSSファイル（例：styles.css, App.cssなど）。
