
# ■実際の作業

以下、アプリケーションインストール後に実際に行った作業

## ファイル名の変更

作成するアプリケーショに合わせて、下記のようにファイル名の修正を行う
「シンボル名称の変更」を使用することで、影響範囲も全て修正する

HelloWorld　→　TodoHeader　：アプリケーションのヘッダー部分


## ヘッダー部分作成

*   vueファイルに記載されているstyleをすべて消し、文言の修正を行う
*   ヘッダー部分に配置されるようにcssをいじる →　[参考](https://www.tohoho-web.com/css/index.htm)

```css
/**下記のようにmediaクエリを使用することで、条件に応じたスタイルを適用させることができる＊*/

/* 幅が 767px 以下であれば */
@media (max-width:767px) { ... }

/* 幅が 768px 以上であれば */
@media (min-width:768px) { ... }

/* 幅が 768px以上 1200px以下であれば */
@media (min-width:768px) and (max-width:1200px) { ... }

/* カラーディスプレイまたはモノクロ印刷であれば */
@media screen and (color), print and (monochrome) { ... }
```

```css
/* 空間に関する設定　*/
margin: 10px;                   /* 上側:10px、右側:10px、下側:10px、左側:10px */
margin: 10px 20px;              /* 上側:10px、右側:20px、下側:10px、左側:20px */
margin: 10px 20px 30px;         /* 上側:10px、右側:20px、下側:30px、左側:20px */
margin: 10px 20px 30px 40px;    /* 上側:10px、右側:20px、下側:30px、左側:40px */
```

## リスト部分作成
*   ヘッダーとデータ部分は、v-forを使用して書きたい
*   その際、カラム幅等個別のスタイル適用をさせたい

    →　[参考](https://techblog.roxx.co.jp/entry/2019/08/15/194652)

---
### ダミーデータとメソッド部分
```javascript
<script lang = "ts">

export default {
  data() {
    return {
        // これの要素分ヘッダーを作成する
        headers: [
            'No', 'Todo', 'Status', 'Button'
        ],
        todos: [
            {No:1, Todo:'やること1', Status:'未着手'},
            {No:2, Todo:'やること2', Status:'未着手'},
            {No:3, Todo:'やること3', Status:'未着手'},
            {No:4, Todo:'やること4', Status:'完了'}
        ]
    }
  },
  methods: {
    // thタグで回している要素の名前を引数として、小文字にした文字列（class名）を返すメソッド
    getClass(headerName){
        return headerName.toLowerCase()
    }
  }
}
</script>
```


---
### HTML部分
```html
<!-- テーブルヘッダー -->
<thead>
<!-- v-forの部分：headersの要素分ヘッダー項目を作成し続けるようにする（項目数が変化しても対応が楽）-->
<!-- :class=の部分：class名取得メソッドを、現在の要素を引数にして呼び出す-->
<th v-for="header in headers" :key="header" :class="getClass(header)">
    {{ header }}
</th>
</thead>
```
---
### css部分

```css
/* **classで指定する個別のスタイル** */
/* getClassで取得しやすいように　&　命名規則が明確になるように、ヘッダー項目名の小文字をclass名とした*/
.no{
width: 50px;
}
.todo{
width: 550px;
}
.status{
width: 200px;
}
.button{
width: 200px;
}
```


## コンポーネント間の値の受け渡し
* 1ファイルの情報量を最小限にするため、用途でファイルを分けた
* 上記により、ファイル間で値の受け渡しをする必要が出てきたが、地味に躓くポイントだった
  →　[参考](https://qiita.com/minuro/items/fa3ddd70ace5b99a1f90)

---
### 子コンポーネント側（受け取る側）
```javascript
export default {
  data(){},
  {/* 親コンポーネントから渡されるものを、子コンポーネントではどの型・変数で扱うか定義 */}
  props: {
    todos:{
      type: Array
    }
  },
  methods:{
    hoge(){
      const todo = {No: No++, Todo: this.newTodo, StatusId: 0}
      // このファイルの、propsの中の、todosで定義した配列に、todoを追加
      this.props.todos.push(todo)
      this.newTodo = ''
    }
  }
}

```

---
### 親コンポーネント側（渡す側）
```javascript
// js部分
export default{
  data(){
    // 子コンポーネントに渡す変数を定義しておく
    return{
      todos: Array
    }
  },
  // 親コンポーネント内で呼び出す子コンポーネントを定義
  components: {
    TodoAdd,
    TodoList
  }
}
</script>
```

```html
<template>
  <!-- :(prop名)="(データ名)" -->
  <!-- :(prop名) ⇨ v-bind:prop名の省略形 -->
  <TodoAdd :todos='todos'/>
  <TodoList />
</template>
```


