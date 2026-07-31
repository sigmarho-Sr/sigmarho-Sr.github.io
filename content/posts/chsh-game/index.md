+++
date = '2026-07-29T23:40:58+09:00'
draft = true
title = 'CHSHゲーム'
+++
{{< katex >}}

量子情報理論では, エンタングルメントは情報処理のリソースとして考えられることが多々ある. 今回はCHSHゲーム, およびその古典的な戦略と量子的な戦略を見比べることによって, エンタングルメントのリソースとしての側面をみてみる. 

CHSHゲームは Alice, Bob, そして Referee の3人で行われる. Alice と Bob はゲームの開始から終了まで, お互いに空間的に分断され, いかなる手段でも連絡を取ることはできないものとする. ゲームは以下のように進行する

1. Referee が bit \(x\) および bit \(y\) をそれぞれ一様な確率で決定する.
2. Referee が Alice に \(x\) を, Bob に \(y\) をそれぞれ送信する.
3. Alcie は受け取った \(x\) を基に, bit \(a\) を決定し, Bob も同様に受け取った \(y\) を基に, bit \(b\) を決定する.
4. Alice, Bob は \(a\), \(b\) をそれぞれ Referee に送信する.
5. Referee は これらの bit の間に, \(x \land y = a \oplus b\) が成立しているかを判定する. 成立していた場合は Alice と Bob の勝利である.

Alice と Bob の勝率を計算するために, 以下の関数を導入する. 
$$
V(x,y,a,b)=\begin{cases}
    1 & \text{if $x \land y = a \oplus b$,} \\
    0 & \text{else.}
  \end{cases}
$$
この関数を用いて, Alice と Bob の勝率は,  
$$
\sum_{a,b,x,y}V(x,y,a,b)p_{ABXY}(a,b,x,y)=\sum_{a,b,x,y}V(x,y,a,b)p_{AB|XY}(a,b|x,y)p_{XY}(x,y)
$$
と書くことができる. \(x\) および \(y\) は一様な確率で決定されるから, 
$$
p_{XY}(x,y)=\frac{1}{4}
$$
である. 改めて, Alice と Bob の勝率は,  
$$
\frac{1}{4}\sum_{a,b,x,y}V(x,y,a,b)p_{AB|XY}(a,b|x,y)
$$
と書くことができる. ここで, \(p_{AB|XY}(a,b|x,y)\) は「\(x\) と \(y\) が与えられたときに, \(a\) および \(b\) を選ぶ条件付き確率」だが, これは Alice と Bob がとる戦略に対応する. ここで, \(\lambda\) に値を取る確率変数 \(\Lambda\) を導入する. これは, Alice と Bob がゲームの開始前に共有することができるリソースを表す. これを用いると, Alice と Bob の戦略を
$$
p_{AB|XY}(a,b|x,y)=\int d\lambda\ p_{AB|\Lambda XY}(a,b|\lambda,x,y)p_{\Lambda|XY}(\lambda|x,y)
$$
と, 事前の共有リソースを含む形で表現できる. 

## 古典的な戦略

では, まずは古典的な戦略について考える. 確率変数 \(\Lambda\) の値 \(\lambda\) は Alice と Bob がゲームの開始前に共有しておくものであり, \(x\), \(y\) はそれぞれ独立に一様ランダムに選ばれるため, 確率変数 \(\Lambda\) は bit \(x\), \(y\) に依存することはできない. したがって, \(p_{\Lambda|XY}(\lambda|x,y)\) は
$$
p_{\Lambda|XY}(\lambda|x,y)=p_{\Lambda}(\lambda)
$$
と書くことができる. 

つぎに, Alice と Bob はそれぞれ独立に動くので, \(p_{AB|\Lambda XY}(a,b|\lambda,x,y)\) は
$$
p_{AB|\Lambda XY}(a,b|\lambda,x,y)=p_{A|\Lambda XY}(a|\lambda,x,y)p_{B|\Lambda XY}(b|\lambda,x,y)
$$
と書ける. さらに, Alice は Bob に送られた bit \(y\) を参照することはできないし, Bob も同様に bit \(x\) を参照することはできないので
$$
p_{AB|\Lambda XY}(a,b|\lambda,x,y)=p_{A|\Lambda X}(a|\lambda,x)p_{B|\Lambda Y}(b|\lambda,y)
$$
と書ける. 

以上のことから, 古典的な戦略における確率分布 \(p_{AB|XY}(a,b|x,y)\) は
$$
p_{AB|XY}(a,b|x,y)=\int d\lambda\ p_{A|\Lambda X}(a|\lambda,x)p_{B|\Lambda Y}(b|\lambda,y)p_{\Lambda}(\lambda)
$$
と表せることがわかる. さらに, 任意の確率分布 \(p_{A|\Lambda X}(a|\lambda,x)\) は, \(n\) をその値とするローカルな確率変数 \(N\) と決定論的な二値関数 \(f(a|\lambda,x,n)\) を用いてシミュレートできる（例えば, さいころで特定の目が出たら確定で \(a\) を \(0\) とするというようなルールを設ける, ということ. ここでは確率変数 \(N\) がさいころの出目に, 二値関数 \(f(a|\lambda,x,n)\) がそのルールにそれぞれ対応している）ので, 
$$
p_{A|\Lambda X}(a|\lambda,x)=\int dn\ f(a|\lambda,x,n)p_{N}(n)
$$
と表せる. 同様に, 確率変数 \(M\) と決定論的な二値関数 \(g(b|\lambda,y,m)\) を導入することで,
$$
p_{B|\Lambda Y}(b|\lambda,y)=\int dn\ g(b|\lambda,y,m)p_{M}(m)
$$
と書ける. したがって, 
$$
\begin{align*}p_{AB|XY}&(a,b|x,y)\\&=\int d\lambda\ p_{A|\Lambda X}(a|\lambda,x)p_{B|\Lambda Y}(b|\lambda,y)p_{\Lambda}(\lambda)\\&=\int d\lambda\ \left[\int dn\ f(a|\lambda,x,n)p_{N}(n)\right]\left[\int dn\ g(b|\lambda,y,m)p_{M}(m)\right]p_{\Lambda}(\lambda)\\&=\iiint d\lambda\ dn\ dm\ f(a|\lambda,x,n)g(b|\lambda,y,m)p_{\Lambda}(\lambda)p_{N}(n)p_{M}(m)\end{align*}
$$
と書ける. 最後の表式から, 共有した確率変数 \(\Lambda\) にローカルな確率変数 \(N\) と \(M\) を含めることができることに気が付く. したがって, 古典的戦略における条件付き確率 \(p_{AB|XY}(a,b|x,y)\) は
$$
p_{AB|XY}(a,b|x,y)=\int d\lambda\ f'(a|\lambda,x)g'(b|\lambda,y)p_{\Lambda}(\lambda)
$$
と書ける. ここで, \(f'\) と \(g'\) はそれぞれ \(f\) と \(g\) に関係する決定論的な二値関数である. 勝率の式にこれを代入すれば, 
$$
\begin{align*}\frac{1}{4}&\sum_{a,b,x,y}V(x,y,a,b)p_{AB|XY}(a,b|x,y)\\&=\frac{1}{4}\sum_{a,b,x,y}V(x,y,a,b)\int d\lambda\ f'(a|\lambda,x)g'(b|\lambda,y)p_{\Lambda}(\lambda)\\&=\int d\lambda\ p_{\Lambda}(\lambda)\left[\frac{1}{4}\sum_{a,b,x,y}V(x,y,a,b)f'(a|\lambda,x)g'(b|\lambda,y)\right]\\&\leq \frac{1}{4}\sum_{a,b,x,y}V(x,y,a,b)f'(a|\lambda^{*},x)g'(b|\lambda^{*},y)\end{align*}
$$
を得る. 最後の行の不等号では, 平均値は最大値を超えられないことを用いた. したがって, ある特定の \(\lambda^{*}\) が存在して最後の不等号が成り立つ. この結果から, 古典的戦略における勝率を評価するには決定論的な戦略のみに焦点を当てればよいことがわかる. 

決定論的な戦略を考えるために, \(a_{x}\) を Alice が \(x\) を受け取ったときに返す bit, \(b_{y}\) を Bob が \(y\) を受け取ったときに返す bit とする. \(x\), \(y\) の値に対する勝利条件を以下の表に示す. 

|\(x\)|\(y\)|\(x\land y\)|\(a_{x}\oplus b_{y}\)|
|:---:|:---:|:---:|:---:|:---:|
|\(0\)|\(0\)|\(0\)|\(a_{0}\oplus b_{0}\)|
|\(0\)|\(1\)|\(0\)|\(a_{0}\oplus b_{1}\)|
|\(1\)|\(0\)|\(0\)|\(a_{1}\oplus b_{0}\)|
|\(1\)|\(1\)|\(1\)|\(a_{1}\oplus b_{1}\)|

\(x\land y\) の列の4つの値に対して排他的論理和を取ると常に \(1\) となるが, \(a_{x}\oplus b_{y}\) の列に同じことをすると常に \(0\) となる. 4つの場合すべてにおいて勝利することができる戦略があるならば, この排他的論理和の値は常に等しくなるので, 勝率は  \(1\) とはならない. 最大で4つのうち3つは勝利条件を満たすことができるので, 勝率は
$$
\sum_{a,b,x,y}V(x,y,a,b)p_{ABXY}(a,b,x,y)\leq\frac{3}{4}
$$
を満たさなければならない. 実際に Alice と Bob は \(x\), \(y\) に関係なく, ともに常に \(0\) を返す戦略を取ればこの勝率を達成できる.

## 量子的な戦略

次に, 量子的な戦略について考える. ここでパラメータ \(\lambda\) は共有量子状態 \(\ket{\phi}_{AB}\) に対応する. Alice と Bob は彼らが受け取った入力 \(x\), \(y\) の値に依存する測定を行う. Alice の \(x\) に依存する測定を \(\{\Pi_{a}^{(x)}\}\) とし, Bob の \(y\) に依存する測定を \(\{\Pi_{b}^{(y)}\}\) とする. これを用いると, 条件付き確率分布 \(p_{AB|XY}(a,b|x,y)\) を
$$
p_{AB|XY}(a,b|x,y)=\bra{\phi}_{AB}(\Pi_{a}^{(x)}\otimes\Pi_{b}^{(y)})\ket{\phi}_{AB}
$$
と書くことができる. したがって, 量子論的な戦略における勝率は
$$
\frac{1}{4}\sum_{a,b,x,y}V(x,y,a,b)\bra{\phi}_{AB}(\Pi_{a}^{(x)}\otimes\Pi_{b}^{(y)})\ket{\phi}_{AB}
$$
である. 

共有する量子状態を最大エンタングル状態 \(\ket{\Phi_{2}}\) とすると, 以下の方法で勝率を古典的な戦略の場合よりも高めることができる. 

- \(x=0\)：Alice が Pauli \(Z\) の測定を施し, 測定の結果を \(a\) として送信する. （測定の結果が \(+1\) ならば \(a=0\) とし, 測定の結果が \(-1\) ならば \(a=1\) とする）
- \(x=1\)：Alice が Pauli \(X\) の測定を施し, 測定の結果を \(a\) として送信する.
- \(y=0\)：Bob が \((X+Z)/\sqrt{2}\) の測定を施し, 測定の結果を \(b\) として送信する.
- \(y=1\)：Bob が \((Z-X)/\sqrt{2}\) の測定を施し, 測定の結果を \(b\) として送信する.

入力が \(x\), \(y\) のとき Alice, Bob が測定する物理量をそれぞれ \(A^{(x)}\), \(B^{(y)}\) とし, これらの物理量の積の期待値を \(E(x,y)=\bra{\Phi_{2}}_{AB}A^{(x)}\otimes B^{(y)}\ket{\Phi_{2}}_{AB}\) とする.

\((x,y)=(0,0),(0,1),(1,0)\) のときは, \(a\oplus b=0\), つまり \(a\) と \(b\) の値が等しければ勝利する. これは, 測定値の積が \(1\) であることと同値である. したがってこの条件の下での勝率は, 測定値の積が \(1\) である確率と等しい. \((x,y)=(1,1)\) のときは, \(a\) と \(b\) の値が異なっていれば勝利する. これは, 測定値の積が \(-1\) であることと同値である. したがってこの条件の下での勝率は, 測定値の積が \(-1\) である確率と等しい.

測定値の積が \(1\) である確率を \(p_{+}\), \(-1\) である確率を \(p_{-}\) とすれば,
$$
E(x,y)=p_{+}-p_{-}
$$
である. したがって,
$$
p_{+}=\frac{1+E(x,y)}{2},\quad p_{-}=\frac{1-E(x,y)}{2}
$$
を得る. 

各 \((x,y)\) について \(E(x,y)\) を計算すると
$$
\begin{align*}E(0,0)&=\bra{\Phi_{2}}_{AB}Z\otimes\frac{X+Z}{\sqrt{2}}\ket{\Phi_{2}}_{AB}=\frac{1}{\sqrt{2}}\\E(0,1)&=\bra{\Phi_{2}}_{AB}Z\otimes\frac{Z-X}{\sqrt{2}}\ket{\Phi_{2}}_{AB}=\frac{1}{\sqrt{2}}\\E(1,0)&=\bra{\Phi_{2}}_{AB}X\otimes\frac{X+Z}{\sqrt{2}}\ket{\Phi_{2}}_{AB}=\frac{1}{\sqrt{2}}\\E(1,1)&=\bra{\Phi_{2}}_{AB}X\otimes\frac{Z-X}{\sqrt{2}}\ket{\Phi_{2}}_{AB}=-\frac{1}{\sqrt{2}}\end{align*}
$$
を得る. したがって, \(p_{AB|XY}(a,b|x,y)\) の値は \((x,y)\) の値に依らず
$$
p_{AB|XY}(a,b|x,y)=\frac{1+1/\sqrt{2}}{2}\approx 0.85
$$
となる. 

これは古典的に最適な戦略を用いた場合の勝率である \(3/4=0.75\) を上回っている. 

次に, 今導いた勝率が実は最適であることを示す. この最適値は **Tsirelson 限界** （*Tsirelson's bound*）とよばれている. 

さて, \((x,y)=(0,0),(0,1),(1,0)\) のときは勝率は \(a\) と \(b\) の値が等しいときに勝利する. その確率は
$$
\bra{\phi}_{AB}(\Pi_{0}^{(x)}\otimes\Pi_{0}^{(y)})\ket{\phi}_{AB}+\bra{\phi}_{AB}(\Pi_{1}^{(x)}\otimes\Pi_{1}^{(y)})\ket{\phi}_{AB}
$$
であり, 負ける確率は
$$
\bra{\phi}_{AB}(\Pi_{0}^{(x)}\otimes\Pi_{1}^{(y)})\ket{\phi}_{AB}+\bra{\phi}_{AB}(\Pi_{1}^{(x)}\otimes\Pi_{0}^{(y)})\ket{\phi}_{AB}
$$
と計算できる. したがって, \((x,y)=(0,0),(0,1),(1,0)\) のとき, 勝つ確率から負ける確率を引いた値は, 
$$
\bra{\phi}_{AB}A^{(x)}\otimes B^{(y)}\ket{\phi}_{AB}
$$
と書ける. ここで, オブザーバブル \(A^{(x)}\), \(B^{(y)}\) を
$$
\begin{align*}A^{(x)}&:=\Pi_{0}^{(x)}-\Pi_{1}^{(x)}\\B^{(y)}&:=\Pi_{0}^{(y)}-\Pi_{1}^{(y)}\end{align*}
$$
と定義した. \((x,y)=(1,1)\) のときは, \(a\) と \(b\) の値が異なるときに勝利する. 先ほどと同様に, 勝つ確率から負ける確率を引いた値は, 
$$
-\bra{\phi}_{AB}A^{(1)}\otimes B^{(1)}\ket{\phi}_{AB}
$$
と書ける. 

全ての入力 bit の間で平均化すると, 勝つ確率から負ける確率を引いた値は, 
$$
\frac{1}{4}\bra{\phi}_{AB}C_{AB}\ket{\phi}_{AB}
$$
と書ける. ここで, \(C_{AB}\) を
$$
C_{AB}:=A^{(0)}\otimes B^{(0)}+A^{(0)}\otimes B^{(1)}+A^{(1)}\otimes B^{(0)}-A^{(1)}\otimes B^{(1)}
$$
と定義した. これを2乗すると
$$
C_{AB}^{2}=4I_{AB}-[A^{(0)},A^{(1)}]\otimes[B^{(0)},B^{(1)}]
$$
を得る. \(\infty\)-ノルムを取ると
$$
\begin{align*}\|C_{AB}^{2}\|_{\infty}&=\|4I_{AB}-[A^{(0)},A^{(1)}]\otimes[B^{(0)},B^{(1)}]\|_{\infty}\\&\leq4\|I_{AB}\|_{\infty}+\|[A^{(0)},A^{(1)}]\otimes[B^{(0)},B^{(1)}]\|_{\infty}\\&=4+\|[A^{(0)},A^{(1)}]\|_{\infty}\cdot\|[B^{(0)},B^{(1)}]\|_{\infty}\\&\leq4+2\cdot2=8\end{align*}
$$
を得る. したがって
$$
\|C_{AB}\|_{\infty}\leq\sqrt{8}=2\sqrt{2}
$$
がいえる. 勝つ確率と負ける確率の和が \(1\) であることから勝率は \(\dfrac{1+1/\sqrt{2}}{2}\) より大きくなることはできない.

## 参考文献
- Wilde, Mark M. From classical to quantum Shannon theory. _arXiv preprint arXiv:1106.1445_, 2011.