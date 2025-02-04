通常、関数を定義するには、コード内でどこかにdefキーワードを使用して定義し、必要に応じて呼び出します。

    def sum(a,b):
        return a + b

    a = 1
    b = 2
    c = sum(a,b)
    print(c)

関数をどこかに定義して呼び出す代わりに、Pythonのlambda関数を使用できます。これは、使用する同じ場所にインラインで定義される関数です。これにより、一度だけ使用するためにどこかに関数を宣言し、コードを再訪する必要がありません。

名前を持つ必要がないため、匿名関数とも呼ばれます。lambdaキーワードを使用してlambda関数を定義します。

    your_function_name = lambda inputs : output

上記のsumの例をlambda関数を使って書くと、

    a = 1
    b = 2
    sum = lambda x,y : x + y
    c = sum(a,b)
    print(c)

ここでは、lambda関数を変数**sum**に代入し、引数、つまりaとbを与えると、通常の関数のように機能します。

Exercise
--------
与えられたリスト内の数が奇数であるかどうかをチェックするために、lambda関数を使用してプログラムを書いてください。数が奇数なら「True」、そうでないなら「False」を各要素に対して出力してください。