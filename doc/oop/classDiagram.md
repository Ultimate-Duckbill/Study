# クラス図の基礎

## UMLとは

UML(Unified Modeling Language)の略で、システムを視覚化したり、仕様や設計を文書化したりするための表現方法です。

UMLの仕様は膨大なものなので、興味のある方は下記のサイトを参照してください。
<https://www.uml.org/index.htm>
## クラス図

クラス図(Class Diagram)は、クラスやインスタンス、インターフェースなどの静的な関係を表したもの。
クラス図という名称だが、クラス以外でも使用される。

> クラス図では、関係性は矢印で表されますが、`親クラス->子クラス`という矢印の向きが直感的に理解しやすいかもしれません。しかし、クラス図では実際には`親クラス<-子クラス`という矢印の向きになります。
> これは、クラス図において矢印の向きが「依存関係の向き」を表しているためです。
> 「子は親に依存する」と考えると理解しやすいかもしれません。

## クラス図の使用例

### AがBを使用する

+ Bの内部関数は静的メソッド
+ 使用(Uses)を表現する場合、点線を用いる。
    + 点線は`弱い関連性`を表す
+ クラス図
    ```mermaid
    classDiagram
        classDiagram-direction LR
        A ..> B: Uses
    ```

+ コード例
    ```ts
    class A {
        static hello () {
            // i.
            console.log(B.greeting());
        }
    }
    class B {
        static readonly word: string = 'Hello!';
        // 静的メソッド
        static greeting() {
            return B.word;
        }
    }

    // クラスAのhelloを実行
    A.hello();
    // 出力: Hello!
    ```
    1. クラスBの`greeting`関数を`console.log`する。

### AがBを生成する

+ 生成(Creates)を表現する場合、実線を用いる。
    + 実線は`強い関連性`を表す
+ クラス図
    ```mermaid
    classDiagram
        classDiagram-direction LR
        A --> B: Creates
    ```
+ コード例
    ```ts
    class A {
        static hello () {
            // i.
            const b = new B('Hello!');
            // iii.
            console.log(b.greeting)
        }
    }

    class B {
        // ii.
        constructor(private word:string){}
        // getter
        get greeting () {
            return this.word
        }
    }

    // クラスAのhelloを実行
    A.hello();
    // --> Hello!
    ```

    1. クラスBをインスタンス生成する。その際に値を渡す
    2. コンストラクタで値を受け取る(wordに代入される)
    3. インスタンスBのgreetingのゲッターを使って`console.log`する

