# 第5回講義中課題

ソースコード：[source.c](./source.c)

### 1)

このプログラムの動作直後に数字の3を入力したとき次の問いに答えなさい。

- (ア) スタックを操作するために `switch` 文中から呼び出される関数はどの関数か
- (イ) *(ア)* で呼び出された関数の実行が終了し `main` に戻った時のその関数の戻り値はいくつか
- (ウ) *(ア)* で呼び出された関数の実行が終了したときのスタックポインタの値はいくつか

### 2)

スタックに「47」「42」「35」「11」「24」の順で値が積まれ、下線部①の部分でプログラムが入力待ちの時、次の問いに答えない。

- (ア) `s.ptr` と `s.stk[4]` の値はいくつか
- (イ) ピークを指示し、ピークしたデータとして表示される値はいくつか
- (ウ) *(イ)* でピークを指示し、ピークしたデータの値を表示したあと、再度下線部①の部分でプログラムが入力待ちのとき `s.stk[s.ptr -5]` の値はいくつか

### 3)

[第3回講義中課題](../prob3post) で用いた「身体検査データを定義する」以下の構造体 PhysCheck 型を、スタックで扱えるようにする「身体検査データ型スタックを実現する構造体」PhysCheckStack 型を定義し、「スタックの実現例」のプログラム中の IntStack 型を PhysCheckStack 型に変更しても正しく動作するようにする。以下では、PhysCheckStack 型の定義と、変更したプログラム中の Push 関数と Pop 関数を答える。

```c
typedef struct {
    double vision:
    int height;
} Body;

typedef struct {
    Body body;
    char name[20];
} PhysCheck;
```

## 提出

```
1)
(ア) Peek 
(イ) -1
(ウ) 0

2)
(ア) s.ptr：5, s.stk[4]：24
(イ) 24
(ウ) 47

3)
int Push(PhysCheckStack *s, PhysCheck x) {
    if (s->ptr >= s->max) return -1;
    s->stk[s->ptr] = x;
    s->ptr++;
    return 0;
}

int Pop(PhysCheckStack *s, PhysCheck *x) {
    if (s->ptr <= 0) return -1;
    s->ptr--;
    *x = s->stk[s->ptr];
    return 0;
}
```