# 並列処理で高速化してみよう！

画像検出などを行うと処理時間が長く十分な結果が得られないことがある

ここでは、CPUの各部分に対して別々の処理をさせ、分担させることで効率化をするということをする

## 使用するライブラリについて

今回はpythonの標準ライブラリであるmultiprocessingを利用する

## 実際のコード

今回は、変数aに1を足し続ける関数と変数bから1を引き続ける関数の2つを同時に実行する

本来であれば、1を足す→1を引くというコードを書かない限り片方しか実行できない（処理の終わりがないため）

しかし、multiprocessingを使うことでこの2つを同時に実行することができる

```
from multiprocessing import Process, Pipe
import time

global num
num = 0
dummy = 0

def task_1():

    a = 0

    while(1):

        a += 1
        time.sleep(0.01)

def task_2():

    b = 0

    while(1):

        b += -1
        time.sleep(0.01)


if __name__ == '__main__':
  
    t1 = Process(target=task_1)
    t2 = Process(target=task_2)

    t1.start()
    t2.start()

    t1.join()
    t2.join()
 ```
