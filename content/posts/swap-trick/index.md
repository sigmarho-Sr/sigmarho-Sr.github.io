+++
date = '2026-02-05T17:00:31+09:00'
draft = false
title = 'スワップ・トリックの証明'
+++
{{< katex >}}

量子情報理論でよく用いられる**スワップ・トリック**（*swap trick*）を証明する. 

>[!tip] スワップ・トリック
行列 \(M,N\in\mathcal{B}(\mathcal{H})\) に対して, 以下が成り立つ. 
$$
\mathrm{Tr}[(M\otimes N)F]=\mathrm{Tr}[MN]
$$

ここで, 演算子 \(F\in\mathcal{B}(\mathcal{H}^{\otimes2})\) は**スワップ演算子**（*swap operator*）で, \(\mathcal{H}\) の正規直交基底 \(\{\ket{e_{j}}\}_{j}^{\dim\mathcal{H}-1}\) を用いて以下で定義される.
$$
F=\sum_{j,k=0}^{\dim\mathcal{H}-1}\ket{e_{j}}\bra{e_{k}}\otimes\ket{e_{k}}\bra{e_{j}}
$$

ここでは正規直交基底を用いてスワップ演算子を定義したが, 実はスワップ演算子は正規直交基底の選び方に依らない. このことは後で説明する.

スワップ・トリックは直接計算することで示すことができるが, 今回は少し遠回りな方法で示すことにする. そのために, まずは置換ユニタリを導入する.

\(\mathfrak{S}_{t}\) を \(t\) 次対称群とする. 置換 \(\sigma\in\mathfrak{S}_{t}\) を用いて, テンソル積空間 \(\mathcal{H}^{\otimes t}\) 上の置換ユニタリ \(V_{\sigma}\in\mathrm{U}(\mathcal{H}^{\otimes t})\) を
$$
V_{\sigma}:=\sum_{j_{1},\dots,j_{t}=0}^{\dim\mathcal{H}-1}\ket{e_{j_{1}}}\bra{e_{j_{\sigma(1)}}}\otimes\cdots\otimes\ket{e_{j_{t}}}\bra{e_{j_{\sigma(t)}}}
$$
と定義する. 行列 \(M_{s}\in\mathcal{B}(\mathcal{H})\)（\(s=1,2,\dots,t\)）に対して,
$$
V_{\sigma}(M_{1}\otimes\cdots\otimes M_{t})V_{\sigma}^{\dagger}=M_{\sigma^{-1}(1)}\otimes\cdots\otimes M_{\sigma^{-1}(t)}
$$
が成り立つ：
$$
\begin{align*}V_{\sigma}(M_{1}\otimes\cdots\otimes M_{t})V_{\sigma}^{\dagger}&=\sum_{\substack{j_{1},\dots,j_{t}\\k_{1},\dots,k_{t}}}\bigotimes_{s=1}^{t}\braket{e_{j_{\sigma(s)}}|M_{s}|e_{k_{\sigma(s)}}}\ket{e_{j_{s}}}\bra{e_{k_{s}}}\\&=\sum_{\substack{j_{1},\dots,j_{t}\\k_{1},\dots,k_{t}}}\bigotimes_{s=1}^{t}(M_{\sigma^{-1}(s)})_{j_{s}k_{s}}\ket{e_{j_{s}}}\bra{e_{k_{s}}}\\&=M_{\sigma^{-1}(1)}\otimes\cdots\otimes M_{\sigma^{-1}(t)}\end{align*}
$$
したがって, 置換ユニタリはテンソル積空間の各々のHilbert空間を置換するものであることがわかる. さらに, \(M_{1}=\cdots=M_{t}=U\in\mathrm{U}(\mathcal{H})\) とすると,
$$
(U^{\otimes t})^{\dagger}V_{\sigma}U^{\otimes t}=V_{\sigma}
$$
を得る. これは, 置換ユニタリの正規直交基底をユニタリで変換しても不変であることを意味する. すなわち, 置換ユニタリは正規直交基底の選び方には依存しない. スワップ演算子は \(t=2\) の場合の置換ユニタリの一つなので, これもまた正規直交基底の選び方に依存しない.

置換ユニタリは以下の補題を満たす.

>[!tip] 補題
行列 \(M_{s}\in\mathcal{B}(\mathcal{H})\) と長さ \(l\) の巡回置換
$$
c=[\gamma\quad c(\gamma)\quad\cdots\quad c^{l}(\gamma)]
$$
に対して, 以下が成り立つ.
$$
\mathrm{Tr}[(M_{1}\otimes\cdots\otimes M_{t})V_{c}^{\dagger}]=\mathrm{Tr}[M_{\gamma}M_{c(\gamma)}\cdots M_{c^{l}(\gamma)}]\prod_{s\neq\gamma,c(\gamma),\dots,c^{l}(\gamma)}\mathrm{Tr}[M_{s}]
$$

**証明**
\(M_{s}=\sum_{i,j}m_{ij}^{(s)}\ket{e_{i}}\bra{e_{j}}\) と表す. このとき,
$$
\begin{align*}(M_{1}\otimes\cdots\otimes M_{t})V_{c}^{\dagger}&=\sum_{\substack{i_{1},\dots,i_{t}\\j_{1},\dots,j_{t}\\k_{1},\dots,k_{t}}}\bigotimes_{s=1}^{t}m_{i_{s}j_{s}}^{(s)}\delta_{j_{s}k_{c(s)}}\ket{e_{i_{s}}}\bra{e_{k_{s}}}\\&=\sum_{\substack{i_{1},\dots,i_{t}\\j_{1},\dots,j_{t}}}\bigotimes_{s=1}^{t}m_{i_{s}j_{s}}^{(s)}\ket{e_{i_{s}}}\bra{e_{j_{c^{-1}(s)}}}\end{align*}
$$
なので,
$$
\begin{align*}\mathrm{Tr}[(M_{1}\otimes\cdots\otimes M_{t})V_{c}^{\dagger}]&=\sum_{\substack{i_{1},\dots,i_{t}\\j_{1},\dots,j_{t}}}\prod_{s=1}^{t}m_{i_{s}j_{s}}^{(s)}\delta_{i_{s}j_{c^{-1}(s)}}\\&=\sum_{i_{1},\dots,i_{t}}\prod_{s=1}^{t}m_{i_{s}i_{c(s)}}^{(s)}\\&=\sum_{i_{1},\dots,i_{t}}m_{i_{\gamma}i_{c(\gamma)}}^{(\gamma)}m_{i_{c(\gamma)}i_{c^{2}(\gamma)}}^{(c(\gamma))}\cdots m_{i_{c^{l}(\gamma)}i_{\gamma}}^{(c^{l}(\gamma))}\prod_{s\neq\gamma,c(\gamma),\dots,c^{l}(\gamma)}m_{i_{s}i_{s}}^{(s)}\\&=\mathrm{Tr}[M_{\gamma}M_{c(\gamma)}\cdots M_{c^{l}(\gamma)}]\prod_{s\neq\gamma,c(\gamma),\dots,c^{l}(\gamma)}\mathrm{Tr}[M_{s}]\end{align*}
$$
を得る. （証明終了）

任意の置換は互いに素な巡回置換の積で一意に表すことができるので, この補題は任意の置換に拡張できる. すなわち,
$$
\sigma=[\gamma\quad c(\gamma)\quad\cdots\quad c^{l}(\gamma)] [\beta\quad b(\beta)\quad\cdots\quad b^{m}(\beta)]\cdots\
$$
と表せるとき,
$$
\mathrm{Tr}[(M_{1}\otimes\cdots\otimes M_{t})V_{\sigma}^{\dagger}]=\mathrm{Tr}[M_{\gamma}M_{c(\gamma)}\cdots M_{c^{l}(\gamma)}]\mathrm{Tr}[M_{\beta}M_{b(\beta)}\cdots M_{b^{m}(\beta)}]\cdots
$$
が成り立つ. このような計算方法をレプリカ法というようである.

スワップ演算子 \(F\) は \(t=2\) のときの置換 \([1\quad2]\) の置換ユニタリだから
$$
\mathrm{Tr}[(M\otimes N)F]=\mathrm{Tr}[MN]
$$
が成り立つ.

## 参考文献
- 中田芳史. 量子情報理論―情報から物理現象の理解まで―. 朝倉書店, 2024.