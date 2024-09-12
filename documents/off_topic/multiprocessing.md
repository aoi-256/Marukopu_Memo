# 並列処理で高速化してみよう！

画像検出などを行うと処理時間が長く十分な結果が得られないことがある

ここでは、CPUの各部分に対して別々の処理をさせ、分担させることで効率化をするということをする

## 使用するライブラリについて

今回はpythonの標準ライブラリであるmultiprocessingを利用する

## 実際のコード

今回は、変数aに1を足し続ける関数と変数bから1を引き続ける関数の2つを同時に実行する

本来であれば、1を足す→1を引くというコードを書かない限り片方しか実行できない（処理の終わりがないため）

しかし、multiprocessingを使うことでこの2つを同時に実行することができる

この方法では、任意の名前のProcessを生成し、1つの関数とその変数を渡すことができる

そのため、やってほしい処理を関数にまとめておく必要がある

今回は簡単のため、関数内で変数を宣言しwhileを使ったループを作成している


```
from multiprocessing import Process, Pipe
import time

def task_1():

    a = 0
    while(1):
        a += 1
        print(a)
        time.sleep(0.01)   

def task_2():

    b = 0
    while(1):
        b += -1
        print(b)
        time.sleep(0.01)

if __name__ == '__main__':

    # Processの作成 t1は好きな名前にできる　targetに実行したい関数を指定する
    t1 = Process(target=task_1)   
    t2 = Process(target=task_2)

    # Processの開始 
    t1.start()
    t2.start()

    # Processの終了待機（今回は無限ループなので実際には使っていない）
    t1.join()
    t2.join()
 ```
