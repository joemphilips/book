<!-- ## Vectors -->

## ベクタ型

<!-- The first collection type we’ll look at is `Vec<T>`, also known as a *vector*. -->
<!-- Vectors allow us to store more than one value in a single data structure that -->
<!-- puts all the values next to each other in memory. Vectors can only store values -->
<!-- of the same type. They are useful in situations in which you have a list of -->
<!-- items, such as the lines of text in a file or the prices of items in a shopping -->
<!-- cart. -->

最初に見るコレクションは、`Vec<T>`であり、*ベクタ型*としても知られています。ベクタ型は、
メモリ上に値を隣り合わせに並べる単独のデータ構造に2つ以上の値を保持させてくれます。
ベクタ型には、同じ型の値しか保持できません。要素のリストがあるような場面で有用です。
例えば、テキストファイルの各行とか、ショッピングカートのアイテムの価格などです。

<!-- ### Creating a New Vector -->

### 新しいベクタ型を生成する

<!-- To create a new, empty vector, we can call the `Vec::new` function as shown in -->
<!-- Listing 8-1: -->

新しい空のベクタ型を作るには、リスト8-1に示されたように、`Vec::new`関数を呼ぶことができます。

```rust
let v: Vec<i32> = Vec::new();
```

<!-- <span class="caption">Listing 8-1: Creating a new, empty vector to hold values -->
<!-- of type `i32`</span> -->

<span class="caption">リスト8-1: 新しい空のベクタ型を生成して`i32`型の値を保持する</span>

<!-- Note that we added a type annotation here. Because we aren’t inserting any -->
<!-- values into this vector, Rust doesn’t know what kind of elements we intend to -->
<!-- store. This is an important point. Vectors are implemented using generics; -->
<!-- we’ll cover how to use generics with your own types in Chapter 10. For now, -->
<!-- know that the `Vec<T>` type provided by the standard library can hold any type, -->
<!-- and when a specific vector holds a specific type, the type is specified within -->
<!-- angle brackets. In Listing 8-1, we’ve told Rust that the `Vec<T>` in `v` will -->
<!-- hold elements of the `i32` type. -->

こちらには、型注釈を付け足したことに注目してください。このベクタ型に対して、何も値を挿入していないので、
コンパイラには、どんなデータを保持させるつもりなのかわからないのです。これは重要な点です。ベクタ型は、
ジェネリクスを使用して実装されているのです; 独自の型でジェネリクスを使用する方法については、
第10章で解説します。今は、標準ライブラリにより提供されている`Vec<T>`型は、どんな型でも保持でき、
特定のベクタ型が特定の型を保持するとき、その型は山かっこ内に指定されることを知っておいてください。
リスト8-1では、コンパイラに`v`の`Vec<T>`は、`i32`型の要素を保持すると指示しました。

<!-- In more realistic code, Rust can often infer the type of value we want to store -->
<!-- once we insert values, so you rarely need to do this type annotation. It’s more -->
<!-- common to create a `Vec<T>` that has initial values, and Rust provides the -->
<!-- `vec!` macro for convenience. The macro will create a new vector that holds the -->
<!-- values we give it. Listing 8-2 creates a new `Vec<i32>` that holds the values -->
<!-- `1`, `2`, and `3`: -->

より現実的なコードでは、一旦値を挿入したら、コンパイラは保持させたい値の型をしばしば推論できるので、
この型注釈をすることは滅多にありません。初期値のある`Vec<T>`を生成する方が一般的ですし、
Rustには、利便性のために`vec!`というマクロも用意されています。このマクロは、
与えた値を保持する新しいベクタ型を生成します。リスト8-2では、`1`、`2`、`3`という値を持つ新しい`Vec<i32>`を生成しています:

```rust
let v = vec![1, 2, 3];
```

<!-- <span class="caption">Listing 8-2: Creating a new vector containing -->
<!-- values</span> -->

<span class="caption">リスト8-2: 値を含む新しいベクタ型を生成する</span>

<!-- Because we’ve given initial `i32` values, Rust can infer that the type of `v` -->
<!-- is `Vec<i32>`, and the type annotation isn’t necessary. Next, we’ll look at how -->
<!-- to modify a vector. -->

初期値の`i32`値を与えたので、コンパイラは、`v`の型が`Vec<i32>`であると推論でき、型注釈は必要なくなりました。
次は、ベクタ型を変更する方法を見ましょう。

<!-- ### Updating a Vector -->

### ベクタ型を更新する

<!-- To create a vector and then add elements to it, we can use the `push` method as -->
<!-- shown in Listing 8-3: -->

ベクタ型を生成し、要素を追加するには、リスト8-3に示したように、`push`メソッドを使用できます。

```rust
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```

<!-- <span class="caption">Listing 8-3: Using the `push` method to add values to a -->
<!-- vector</span> -->

<span class="caption">リスト8-3: `push`メソッドを使用してベクタ型に値を追加する</span>

<!-- As with any variable, as discussed in Chapter 3, if we want to be able to -->
<!-- change its value, we need to make it mutable using the `mut` keyword. The -->
<!-- numbers we place inside are all of type `i32`, and Rust infers this from the -->
<!-- data, so we don’t need the `Vec<i32>` annotation. -->

あらゆる変数同様、第3章で議論したように、値を変化させたかったら、`mut`キーワードで可変にする必要があります。
中に配置する数値は全て`i32`型であり、コンパイラはこのことをデータから推論するので、
`Vec<i32>`という注釈は必要なくなります。

<!-- ### Dropping a Vector Drops Its Elements -->

### ベクタ型をドロップすれば、要素もドロップする

<!-- Like any other `struct`, a vector will be freed when it goes out of scope, as -->
<!-- annotated in Listing 8-4: -->

他のあらゆる`構造体`同様、ベクタ型もスコープを抜ければ、解放されます。リスト8-4に注釈したようにね:

<!-- ```rust -->
<!-- { -->
<!--     let v = vec![1, 2, 3, 4]; -->

<!--     // do stuff with v -->

<!-- } // <- v goes out of scope and is freed here -->
<!-- ``` -->

```rust
{
    let v = vec![1, 2, 3, 4];

    // vで作業をする

} // <- vはここでスコープを抜け、解放される
```

<!-- <span class="caption">Listing 8-4: Showing where the vector and its elements -->
<!-- are dropped</span> -->

<span class="caption">リスト8-4: ベクタ型とその要素がドロップされる箇所を示す</span>

<!-- When the vector gets dropped, all of its contents will also be dropped, meaning -->
<!-- those integers it holds will be cleaned up. This may seem like a -->
<!-- straightforward point but can get a bit more complicated when we start to -->
<!-- introduce references to the elements of the vector. Let’s tackle that next! -->

ベクタ型がドロップされると、その中身もドロップされます。つまり、保持されていた整数値が、
片付けられるということです。これは一見単純な点に見えるかもしれませんが、ベクタの要素への参照を導入した途端、
もうちょっと複雑になる可能性を秘めています。次は、それに挑んでいきましょう！

<!-- ### Reading Elements of Vectors -->

### ベクタ型の要素を読む

<!-- Now that you know how to create, update, and destroy vectors, knowing how to -->
<!-- read their contents is a good next step. There are two ways to reference a -->
<!-- value stored in a vector. In the examples, we’ve annotated the types of the -->
<!-- values that are returned from these functions for extra clarity. -->

もうベクタ型を生成し、更新し、破壊する方法を知ったので、コンテンツを読む方法を知るのはいいステップアップです。
ベクタ型に保持された値を参照する方法は2つあります。例では、さらなる明瞭性を求めて、
これらの関数から返る値の型を注釈しました。

<!-- Listing 8-5 shows both methods of accessing a value in a vector either with -->
<!-- indexing syntax or the `get` method: -->

リスト8-5に示したのは、両メソッドがベクタ型の値に対して、添字記法と`get`メソッドによりアクセスするところです:

```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
let third: Option<&i32> = v.get(2);
```

<!-- <span class="caption">Listing 8-5: Using indexing syntax or the `get` method to -->
<!-- access an item in a vector</span> -->

<span class="caption">リスト8-5: 添字記法か`get`メソッドを使用してベクタ型の要素にアクセスする</span>

<!-- Note two details here. First, we use the index value of `2` to get the third -->
<!-- element: vectors are indexed by number, starting at zero. Second, the two -->
<!-- different ways to get the third element are by using `&` and `[]`, which gives -->
<!-- us a reference, or by using the `get` method with the index passed as an -->
<!-- argument, which gives us an `Option<&T>`. -->

ここでは、2つのことに気付いてください。まず、3番目の要素を得るのに`2`という添え字の値を使用していることです:
ベクタ型は、数値により順序付けされ、添え字は0から始まります。2番目に、3番目の要素を得る2つの方法は、
`&`と`[]`を使用して参照を得るものと、番号を引数として`get`メソッドに渡して、`Option<&T>`を得るものということです。

<!-- The reason Rust has two ways to reference an element is so you can choose how -->
<!-- the program behaves when you try to use an index value that the vector doesn’t -->
<!-- have an element for. As an example, what should a program do if it has a vector -->
<!-- that holds five elements and then tries to access an element at index 100, as -->
<!-- shown in Listing 8-6: -->

Rustに要素を参照する方法が2通りある理由は、ベクタ型に要素が含まれない番号の値を使用しようとした時に、
プログラムの振る舞いを選択できるようにするためです。例として、ベクタ型に5つ要素があり、
番号100の要素にアクセスを試みた場合、プログラムはどう振る舞うべきでしょうか？リスト8-6に示したようにね:

```rust,should_panic
let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100];
let does_not_exist = v.get(100);
```

<!-- <span class="caption">Listing 8-6: Attempting to access the element at index -->
<!-- 100 in a vector containing 5 elements</span> -->

<span class="caption">リスト8-6: 5つの要素を含むベクタ型の100番目の要素にアクセスしようとする</span>

<!-- When you run this code, the first `[]` method will cause a `panic!` because it -->
<!-- references a nonexistent element. This method is best used when you want your -->
<!-- program to consider an attempt to access an element past the end of the vector -->
<!-- to be a fatal error that crashes the program. -->

このコードを走らせると、最初の`[]`メソッドは`panic!`を引き起こします。存在しない要素を参照しているからです。
このメソッドは、プログラムがベクタの終端を超えて要素にアクセスしようしたことを、
プログラムをクラッシュさせるような重大なエラーとして捉えてほしい場合に最適です。

<!-- When the `get` method is passed an index that is outside the vector, it returns -->
<!-- `None` without panicking. You would use this method if accessing an element -->
<!-- beyond the range of the vector happens occasionally under normal circumstances. -->
<!-- Your code will then have logic to handle having either `Some(&element)` or -->
<!-- `None`, as discussed in Chapter 6. For example, the index could be coming from -->
<!-- a person entering a number. If they accidentally enter a number that’s too -->
<!-- large and the program gets a `None` value, you could tell the user how many -->
<!-- items are in the current `Vec` and give them another chance to enter a valid -->
<!-- value. That would be more user-friendly than crashing the program due to a typo! -->

`get`メソッドがベクタ外の番号を渡されると、パニックすることなく`None`を返します。
普通の状態でも、ベクタの範囲外にアクセスする可能性がある場合に、このメソッドを使用することになるでしょう。
そうしたら、コードには`Some(&element)`か`None`を扱うロジックが存在することになります。そう、
第6章で議論したように。例えば、番号は人間に数値を入力してもらうことで得ることもできます。
もし大きすぎる値を誤って入力し、プログラムが`None`値を得てしまったら、現在`Vec`に幾つ要素があるかをユーザに教え、
再度正しい値を入力してもらうことができるでしょう。その方が、タイプミスでプログラムをクラッシュさせるより、
ユーザに優しくなるでしょう。

<!-- #### Invalid References -->

#### 無効な参照

<!-- When the program has a valid reference, the borrow checker enforces the -->
<!-- ownership and borrowing rules (covered in Chapter 4) to ensure this reference -->
<!-- and any other references to the contents of the vector remain valid. Recall the -->
<!-- rule that states we can’t have mutable and immutable references in the same -->
<!-- scope. That rule applies in Listing 8-7 where we hold an immutable reference to -->
<!-- the first element in a vector and try to add an element to the end: -->

プログラムに有効な参照がある場合、borrow checker(借用精査機)は(第4章で解説しましたが)、
所有権と借用規則を強制し、ベクタ型の中身へのこの参照や他のいかなる参照も有効であり続けることを保証してくれます。
同一スコープ上では、可変と不変な参照を同時には存在させられないというルールを思い出してください。
このルールはリスト8-7にも適用され、リスト8-7ではベクタの最初の要素への不変参照を保持し、
終端に要素を追加しようとしています:

```rust,ignore
let mut v = vec![1, 2, 3, 4, 5];

let first = &v[0];

v.push(6);
```

<!-- <span class="caption">Listing 8-7: Attempting to add an element to a vector -->
<!-- while holding a reference to an item</span> -->

<span class="caption">リスト8-7: 要素への参照を保持しつつ、ベクタに要素を追加しようとする</span>

<!-- Compiling this code will result in this error: -->

このコードをコンパイルすると、こんなエラーになります:

```text
error[E0502]: cannot borrow `v` as mutable because it is also borrowed as
immutable
(エラー: 不変としても借用されているので、`v`を可変で借用できません)
  |
4 | let first = &v[0];
  |              - immutable borrow occurs here
  |              (不変借用はここで発生しています)
5 |
6 | v.push(6);
  | ^ mutable borrow occurs here
  |  (可変借用は、ここで発生しています)
7 | }
  | - immutable borrow ends here
  |   (不変借用はここで終了しています)
```

<!-- The code in Listing 8-7 might look like it should work: why should a reference -->
<!-- to the first element care about what changes at the end of the vector? The -->
<!-- reason behind this error is due to the way vectors work: adding a new element -->
<!-- onto the end of the vector might require allocating new memory and copying the -->
<!-- old elements to the new space if there isn’t enough room to put all the -->
<!-- elements next to each other where the vector was. In that case, the reference -->
<!-- to the first element would be pointing to deallocated memory. The borrowing -->
<!-- rules prevent programs from ending up in that situation. -->

リスト8-7のコードは、一見動くはずのように見えるかもしれません: なぜ、最初の要素への参照が、
ベクタの終端への変更を気にかける必要があるのでしょうか？このエラーの背後にある理由は、
ベクタの動作法にあります: 新規要素をベクタの終端に追加すると、ベクタが存在した位置に隣り合って要素を入れるだけの領域がなかった場合に、
メモリの新規確保をして古い要素を新しいスペースにコピーする必要があるかもしれないからです。
その場合、最初の要素を指す参照は、解放されたメモリを指すことになるでしょう。借用規則により、
そのような場面にならないよう回避されるのです。

<!--  Note: For more on the implementation details of the `Vec<T>` type, see “The -->
<!--  Nomicon” at https://doc.rust-lang.org/stable/nomicon/vec.html. -->

> 注釈: `Vec<T>`の実装に関する詳細については、https://doc.rust-lang.org/stable/nomicon/vec.htmlの、
> "The Nomicon"を参照されたし。

<!-- ### Iterating Over the Values in a Vector -->

### ベクタの値を走査する

<!-- If we want to access each element in a vector in turn, rather than using -->
<!-- indexing to access one element, we can iterate through all of the elements. -->
<!-- Listing 8-8 shows how to use a `for` loop to get immutable references to each -->
<!-- element in a vector of `i32` values and print them out: -->

ベクタの要素に順番にアクセスしたいなら、添え字で1要素にアクセスするのではなく、全要素を走査することができます。
リスト8-8で`for`ループを使い、`i32`のベクタの各要素に対する不変な参照を得て、それらを出力する方法を示しています:

```rust
let v = vec![100, 32, 57];
for i in &v {
    println!("{}", i);
}
```

<!-- <span class="caption">Listing 8-8: Printing each element in a vector by -->
<!-- iterating over the elements using a `for` loop</span> -->

<span class="caption">リスト8-8: `for`ループで要素を走査し、ベクタの各要素を出力する</span>

<!-- We can also iterate over mutable references to each element in a mutable vector -->
<!-- if we want to make changes to all the elements. The `for` loop in Listing 8-9 -->
<!-- will add `50` to each element: -->

全要素に変更を加えたかったら、可変なベクタの各要素への可変な参照を走査することもできます。
リスト8-9の`for`ループでは、各要素に`50`を足しています:

```rust
let mut v = vec![100, 32, 57];
for i in &mut v {
    *i += 50;
}
```

<!-- <span class="caption">Listing 8-9: Iterating over mutable references to -->
<!-- elements in a vector</span> -->

<span class="caption">リスト8-9: ベクタの要素への可変な参照を走査する</span>

<!-- In order to change the value that the mutable reference refers to, before we -->
<!-- can use the `+=` operator with `i`, we have to use the dereference operator -->
<!-- (`*`) to get to the value. -->

可変参照が参照する値を変更するには、`i`に対して`+=`演算子を使用する前に、
参照外し演算子(`*`)を使用して値に辿り着かないといけません。

<!-- ### Using an Enum to Store Multiple Types -->

### Enumを使って複数の型を保持する

<!-- At the beginning of this chapter, we said that vectors can only store values -->
<!-- that are the same type. This can be inconvenient; there are definitely use -->
<!-- cases for needing to store a list of items of different types. Fortunately, the -->
<!-- variants of an enum are defined under the same enum type, so when we need to -->
<!-- store elements of a different type in a vector, we can define and use an enum! -->

この章の冒頭で、ベクタは同じ型の値しか保持できないと述べました。これは不便に考えられることもあります;
異なる型の要素を保持する必要性が出てくるユースケースも確かにあるわけです。幸運なことに、
enumのバリアントは、同じenumの型の元に定義されるので、ベクタに異なる型の要素を保持する必要が出たら、
enumを定義して使用することができます！

<!-- For example, let’s say we want to get values from a row in a spreadsheet where -->
<!-- some of the columns in the row contain integers, some floating-point numbers, -->
<!-- and some strings. We can define an enum whose variants will hold the different -->
<!-- value types, and then all the enum variants will be considered the same type, -->
<!-- that of the enum. Then we can create a vector that holds that enum and so, -->
<!-- ultimately, holds different types. We’ve demonstrated this in Listing 8-8: -->

例えば、スプレッドシートの行から値を得たくなったとしましょう。ここで行の列には、整数を含むものや、
浮動小数点数を含むもの、文字列を含むものがあります。バリアントが異なる値の型を保持するenumを定義できます。
そして、このenumのバリアントは全て同じ型、つまり、enumの型と考えられるわけです。それからそのenumを保持するベクタを生成でき、
結果的に異なる型を保持できるようになるわけです。リスト8-8でこれを模擬しています。

```rust
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```

<!-- <span class="caption">Listing 8-8: Defining an `enum` to store values of -->
<!-- different types in one vector</span> -->

<span class="caption">リスト8-8: `enum`を定義して、一つのベクタに異なる型の値を保持する</span>

<!-- The reason Rust needs to know what types will be in the vector at compile time -->
<!-- is so it knows exactly how much memory on the heap will be needed to store each -->
<!-- element. A secondary advantage is that we can be explicit about what types are -->
<!-- allowed in this vector. If Rust allowed a vector to hold any type, there would -->
<!-- be a chance that one or more of the types would cause errors with the -->
<!-- operations performed on the elements of the vector. Using an enum plus a -->
<!-- `match` expression means that Rust will ensure at compile time that we always -->
<!-- handle every possible case, as discussed in Chapter 6. -->

コンパイラがコンパイル時にベクタに入る型を知る必要がある理由は、
各要素を保持するのにヒープ上でズバリどれくらいのメモリが必要になるかを知るためです。副次的な利点は、
このベクタではどんな型が許容されるのか明示できることです。もしRustでベクタがどんな型でも保持できたら、
ベクタの要素に対して行われる処理に対して一つ以上の型がエラーを引き起こす可能性があったでしょう。
enumに加えて`match`式を使うことは、第6章で議論した通り、コンパイル時にありうる場合全てに対処していることをコンパイラが、
確認できることを意味します。

<!-- 第1文がちょっとわからない。特にwriting a program the exhaustive...のところ。いわゆるSVOOかな？ -->

<!-- If you don’t know when you’re writing a program the exhaustive set of types the -->
<!-- program will get at runtime to store in a vector, the enum technique won’t -->
<!-- work. Instead, you can use a trait object, which we’ll cover in Chapter 17. -->

ベクタに実行時に保持される一連の型をプログラムに記述してあげる場合を知らない場合、このenumテクニックはうまくいかないでしょう。
代わりに、トレイトオブジェクトを使用することができ、こちらは第17章で解説します。

<!-- Now that we’ve discussed some of the most common ways to use vectors, be sure -->
<!-- to review the API documentation for all the many useful methods defined on -->
<!-- `Vec` by the standard library. For example, in addition to `push`, a `pop` -->
<!-- method removes and returns the last element. Let’s move on to the next -->
<!-- collection type: `String`! -->

今や、ベクタを使用するべきありふれた方法について議論したので、標準ライブラリで`Vec`に定義されている多くの有益なメソッドについては、
APIドキュメントを確認することを心得てください。例として、`push`に加えて、`pop`メソッドは最後の要素を削除して返します。
次のコレクション型に移りましょう: `String`です！
