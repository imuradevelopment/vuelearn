# 手順
## vueapp
1. [vue create vueapp(プロジェクト名)]
```
・メモ時点での選択肢
default
use yarn
```
2. 作成されたフォルダに移動し、[yarn add firebase]
3. yarn serveでデフォルト画面が起動することを確認
4. [firebaseの作業](#firebase)
5. main.jsにfirebaseから情報をペーストし、firebaseをimport
```javascript
import Vue from 'vue'
import App from './App.vue'
// firebaesのimport
import firebase from 'firebase'

Vue.config.productionTip = false

// firebaseからの情報をペースト
  // Your web app's Firebase configuration
  var firebaseConfig = {
    apiKey: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~",
    authDomain: "~~~~~~~~~~~~~~~~~~~~~",
    databaseURL: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~",
    projectId: "~~~~~~~~~~~~~~~",
    storageBucket: "~~~~~~~~~~~~~~~~~~~~~~~~~",
    messagingSenderId: "~~~~~~~~~~~~",
    appId: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);
  // ペースト範囲↑

new Vue({
  render: h => h(App),
}).$mount('#app')
```
6. scriptタグ上部でfirebaseをimportして.vueでの作業を開始
```javascript
// firebaseインポート
import firebase from 'firebase'
```

## firebase
1. firebaseプロジェクトの追加
```
アナリティクス今回はチェック外す。
```
2. アプリの追加 [WEB</>]
```
Firebase Hostingは設定しない
```
3. スクリプトが出てくるのでコピー
```javascript
<!-- The core Firebase JS SDK is always required and must be listed first -->
<script src="https://www.gstatic.com/firebasejs/7.2.3/firebase-app.js"></script>

<!-- TODO: Add SDKs for Firebase products that you want to use
     https://firebase.google.com/docs/web/setup#available-libraries -->

<script>
  // Your web app's Firebase configuration
  var firebaseConfig = {
    apiKey: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~",
    authDomain: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~",
    databaseURL: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~",
    projectId: "~~~~~~~~~~~~~~~",
    storageBucket: "~~~~~~~~~~~~~~~~~~~~~~~~",
    messagingSenderId: "~~~~~~~~~~~~~~",
    appId: "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);
</script>
```
4. firestoreの作成

## deploy
### firebase初期化
1. firebase init
2. Hostingでスペースエンター
3. firebaseで作成したプロジェクトを選ぶ
4. What do you want to use as your public directory? dist
5. Configure as a single-page app (rewrite all urls to /index.html)? Yes
### build
1. yarn build
2. distができたことを確認
### firebaseにデプロイ
1. firebase deploy

# firestore
- collection
```
コレクション内のドキュメントの名前は一意です。
ユーザー ID などの独自のキーを指定することも、
Cloud Firestore で自動的にランダムな ID を作成することもできます。
ドキュメントの有無によって作成、削除される。
```
- document
  ```json
  ドキュメント内でさらにMapで構造化した例
  alovelace(documentName?ID?)
    name:
      first : "Ada"
      last : "Lovelace"
    born : 1815
  ```
- reference
```
Cloud Firestore のすべてのドキュメントは、データベース内の場所によって一意に識別されます。
```
```javascript
// users(collection)
//     |
//     - alovelace(document)
// コード内でalovelaceを参照するには、その場所への「リファレンス」を作成します。
var alovelaceDocumentRef = db.collection('users').doc('alovelace');
```
```
便宜上、ドキュメントまたはコレクションへのパスを文字列として指定し、
パス コンポーネントをスラッシュ（/）で区切ってリファレンスを作成することもできます。
たとえば、alovelace ドキュメントへのリファレンスは次のように作成します。
```
```javascript
var alovelaceDocumentRef = db.doc('users/alovelace');
```
```
注: コレクション リファレンスとドキュメント リファレンスは、
2 種類の異なるリファレンスで、それぞれ別のオペレーションを実行できます。
たとえば、コレクション リファレンスを使用してコレクション内のドキュメントに対するクエリを実行したり、
ドキュメント リファレンスを使用して個々のドキュメントを読み書きしたりできます。
```


- tree
```
- collection
  |
  - document
    |
    - data(key:value)
    - subcollection
      |
      - document
        |
        - data(key:value)
```

```
◇collection
◆document

◇users
  |
  ◆ user_id_01
  |   |
  |   ◇ todos_id_01
  |   |   |
  |   |   ◆ todo_id_01
  |   |   |   |
  |   |   |   - todo_name:
  |   |   |   |
  |   |   |   - regist_time:
  |   |   |   |
  |   |   |   - complete_time:
  |   |   |   |
  |   |   |   - complete_flag:
  |   |   |   |
  |   |   |   - importance:
  |   |   |
  |   |   - todo_id_02
  |   |   
  |   - todos_id_02
  |
  - user_id_02
```
