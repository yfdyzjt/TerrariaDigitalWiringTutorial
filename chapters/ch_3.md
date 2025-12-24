## 第三章 电路元件

### 3.1 组合逻辑

#### 3.1.1 基本逻辑运算

泰拉瑞亚组合逻辑电路中存在四种基本逻辑运算：**非、异或、与、独热**。其中非和异或使用逻辑灯完成；与和独热使用逻辑门完成。

!!! info
    现实组合逻辑电路中存在三种基本逻辑运算：**与、或、非**。

!!! tip
    线或应用于激活用电器，属于时序逻辑电路，此外组合逻辑电路中并不会使用或门，所以或并不属于组合逻辑电路的基本逻辑运算。

##### 非

$$Y = \lnot A$$

@import "images/3/1/1/not.png"

##### 异或

$$Y = A \oplus B$$

@import "images/3/1/1/xor.png"

##### 与

$$Y = A \land B$$

@import "images/3/1/1/and.png"

##### 独热

$$Y = \mathrm{OneHot}(A, B)$$

@import "images/3/1/1/one-hot.png"

#### 3.1.2 更多逻辑运算

除了基本逻辑结算和前面介绍的常用逻辑运算外，组合逻辑中还有另外一些经常使用的逻辑运算。

##### 比较

比较运算是比较两个变量的大小或关系，当条件成立时输出 1，否则输出 0。

对于两个变量，可以定义六种基本的比较关系：**小于（LT）、大于（GT）、小于等于（LE）、大于等于（GE）、等于（EQ）、不等于（NE）**。它们在所有输入情况下的输出如下表所示：

| > | 输入 | > | > | > | > | > | 输出 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A | B | $A < B$ | $A > B$ | $A <= B$ | $A >= B$ | $A == B$ | $A\ != B$ |
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 |
| 0 | 1 | 1 | 0 | 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 | 1 | 1 | 0 |

!!! info
    与运算只有在所有输入都为 1 时才输出 1，其余情况输出 0：

    $$A_1 \land A_2 \land \cdots \land A_n = \left\{\begin{array}{ll}1 & \textrm{当 } A_1 = A_2 = \cdots = A_n = 1 \textrm{ 时} \\0&\textrm{其他情况}\end{array}\right.$$

    !!! example
        @import "images/3/1/2/and_all_one.png"

        只有在输入 A1 ~ A4 全为 1 时，输出才为 1；其余情况输出 0。

    如果将与运算的所有输入取反，则逻辑变为：所有输入都为 0 时输出 1，否则输出 0：

    $$\lnot A_1 \land \lnot A_2 \land \cdots \land \lnot A_n = \left\{\begin{array}{ll}1 & \textrm{当 } A_1 = A_2 = \cdots = A_n = 0 \textrm{ 时} \\0&\textrm{其他情况}\end{array}\right.$$

    !!! example
        @import "images/3/1/2/and_all_zero.png"

        只有在输入 A1 ~ A4 全为 0 时，输出才为 1；其余情况输出 0。

    若只对部分输入取反，则该逻辑在“未取反的输入为 1，取反的输入为 0”时输出 1，其余情况输出 0：

    $$A_1 \land A_2 \land \cdots \land A_m \land \lnot B_1 \land \lnot B_2 \land \cdots \land \lnot B_n = \left\{\begin{array}{ll}1 & \textrm{当 } A_1 = A_2 = \cdots = A_n = 1 \textrm{ 且} \\ & B_1 = B_2 = \cdots = B_n = 0 \textrm{ 时} \\0&\textrm{其他情况}\end{array}\right.$$

    !!! example
        @import "images/3/1/2/and_half_one.png"

        只有在输入 A1 ~ A2 全为 1 且 B1 ~ B2 全为 0 时，输出才为 1；其余情况输出 0。

    这种只在真值表中某一行输出为 1 的逻辑表达式称为 **最小项**。

    !!! example
        对于三输入逻辑函数，若只希望在 $A=0, B=1, C=1$ 时输出 1，可以使用最小项 $\lnot A \land B \land C$，该表达式仅在这一输入组合下输出 1。

        !!! quote
            @import "images/3/1/2/and_lut.png"

            只有在输入 $A=0, B=1, C=1$ 时，输出才为 1；其余情况输出 0。

    最小项中每个输入逻辑变量都会出现，且只会出现一次；每个变量在最小项中都有“取反”和“不取反”两种情况。因此对于 $n$ 个变量，一共有 $2^n$ 个最小项，恰好对应真值表的每一行。任意输入，都只会有一个最小项输出为 1。

    !!! example
        三输入变量对应的最小项如下：

        | > | > | 输入 | 输出为 1 最小项 |
        | --- | --- | --- | --- |
        | A | B | C | Y |
        | 0 | 0 | 0 | $\lnot A \land \lnot B \land \lnot C$ |
        | 0 | 0 | 1 | $\lnot A \land \lnot B \land C$ |
        | 0 | 1 | 0 | $\lnot A \land B \land \lnot C$ |
        | 0 | 1 | 1 | $\lnot A \land B \land C$ |
        | 1 | 0 | 0 | $A \land \lnot B \land \lnot C$ |
        | 1 | 0 | 1 | $A \land \lnot B \land C$ |
        | 1 | 1 | 0 | $A \land B \land \lnot C$ |
        | 1 | 1 | 1 | $A \land B \land C$ |

        可以看到真值表中某变量为 0，对应最小项中该变量取反；为 1，则不取反。

        !!! quote
            @import "images/3/1/2/and_lut_full.png"

            三输入全部可能的最小项，一共有 $2^3 = 8$ 个最小项。

    当输出为 1 的情况不止一个时，可以将对应的最小项用异或连接。由于任意输入下最多只有一个最小项为 1，异或运算即可正确合并这些情况。这种由异或连接的最小项称为 **最小项之和**，它可以表示任意逻辑函数。

    !!! example
        对于下表所示的三输入逻辑函数：

        | > | > | 输入 | 输出 |
        | --- | --- | --- | --- |
        | A | B | C | Y |
        | 0 | 0 | 0 | 0 |
        | 0 | 0 | 1 | 0 |
        | 0 | 1 | 0 | 0 |
        | 0 | 1 | 1 | 1 |
        | 1 | 0 | 0 | 0 |
        | 1 | 0 | 1 | 1 |
        | 1 | 1 | 0 | 1 |
        | 1 | 1 | 1 | 1 |

        其逻辑表达式可写为：
        
        $$\lnot A \land B \land C \oplus A \land \lnot B \land C \oplus A \land B \land \lnot C \oplus A \land B \land C$$

        对应四个输出为 1 的最小项之和。

        !!! quote
            @import "images/3/1/2/and_lut_all.png"

            满足该真值表对应逻辑函数的电路。

利用最小项之和，可以得到六种比较运算对应的逻辑表达式：

| 运算 | 记号 | 逻辑表达式 |
| --- | --- | --- |
| 小于 | $A < B$ | $\lnot A \land B$ |
| 大于等于 | $A >= B$ | $\lnot (\lnot A \land B)$ |
| 大于 | $A > B$ | $A \land \lnot B$ |
| 小于等于 | $A <= B$ | $\lnot (A \land \lnot B)$ |
| 不等于 | $A\ != B$ | $A \oplus B$ |
| 等于 | $A == B$ | $\lnot (A \oplus B)$ |

@import "images/3/1/2/compare.png"

!!! tip
    可以看到，小于和大于等于、大于和小于等于、不等于和等于两两互为取反；小于和大于、小于等于和大于等于的区别是交换两个输入。在比较电路中，常利用这一性质减少所需的逻辑门数量。

    !!! quote
        @import "images/3/1/2/compare_all.png"

        * **NOT OUT** 控制是否对输出取反，以在小于（**LT**）和大于等于（**GE**）、大于（**GT**）和小于等于（**LE**）、等于（**EQ**）和不等于（**NE**）间切换；
        * **SW IN** 交换两个输入，以在小于（**LT**）和大于（**GT**）、大于等于（**GE**）和小于等于（**LE**）间切换；

##### 乘（MUL）

两个变量乘运算的逻辑表达式为：

$$A \cdot B$$

!!! info
    读作 A 乘 B。

或者简写为：

$$AB$$

$n$ 个变量乘运算的逻辑表达式为：

$$A_1 \cdot A_2 \cdot \cdots \cdot A_n$$

或者简写为：

$$A_1 A_2 \cdots A_n$$

由乘法关系：

$0 \cdot 0 = 0$
$0 \cdot 1 = 0$
$1 \cdot 0 = 0$
$1 \cdot 1 = 1$

可列出真值表：

| > | 输入 | 输出 |
| --- | --- | --- |
| A | B | Y |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

!!! tip
    可以发现与运算就是乘法运算。

    $$A \cdot B = A \land B$$

    @import "images/3/1/2/mul.png"

!!! info
    任何数乘以 0 等于 0，任何数乘以 1 等于其本身。

    $$0 \cdot A = 0$$

    $$1 \cdot A = A$$
    
    @import "images/3/1/2/mul_0_1.png"

    任何数乘以本身等于其本身。

    $$A \cdot A = A$$

    易得：

    $$A \cdot A \cdot \cdots \cdot A = A$$

    !!! tip
        证明可通过观察真值表完成。

    @import "images/3/1/2/mul_self.png"

##### 加（ADD）、减（SUB）

两个变量加运算的逻辑表达式为：

$$A + B$$

!!! info
    读作 A 加 B。

$n$ 个变量加运算的逻辑表达式为：

$$A_1 + A_2 + \cdots + A_n$$

!!! question
    $$1 + 1 = \ ?$$

    如果是在实数域，我们可以很容易的说出 $1 + 1 = 2$ ，但是在逻辑变量中并没有 $2$。实际上，在逻辑运算中 $1 + 1 = 0$。

    我们可以用两种方式理解这个结果：

    * 如果是有进位加法 $(1 + 1 = 10)_2$，由于逻辑函数只有一位输出，所以抛弃高位的 $1$，只保留低位的 $0$；
    * 加法可以理解为在数轴上从一个加数出发，前进另一个加数的距离，对于一个只有 $0$ 和 $1$ 首尾相连的循环数轴，如果从 $1$ 出发前进 $1$，就会到达 $0$。

    $$\cdots \xrightarrow{+1} 1 \xrightarrow{+1} 0 \xrightarrow{+1} 1 \xrightarrow{+1} 0 \xrightarrow{+1} 1 \xrightarrow{+1} 0 \xrightarrow{+1} 1 \xrightarrow{+1} \cdots$$

由加法关系：

$0 + 0 = 0$
$0 + 1 = 1$
$1 + 0 = 1$
$1 + 1 = 0$

可列出真值表：

| > | 输入 | 输出 |
| --- | --- | --- |
| A | B | Y |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

!!! tip
    可以发现异或运算就是加法运算。

    $$A + B = A \oplus B$$

    @import "images/3/1/2/add.png"

    !!! tip
        双输入异或和独热等价，为便于理解，图中包括使用双灯异或门实现的异或逻辑。

        $$A \oplus B = \mathrm{OneHot}(A, B)$$

!!! info
    任何数加 0 等于其本身，任何数加 1 等于其本身的非。

    $$A + 0 = A$$

    $$A + 1 = \lnot A$$

    @import "images/3/1/2/add_0_1.png"

    !!! tip
        线异或两项中的一项恒为 1 相当于线非。

    任何数加本身等于 0。

    $$A + A = 0$$

    易得：

    $$\underbrace{A + A + \cdots + A}_{n} = \begin{cases} 0, & n = 2k, \\[4pt] A, & n = 2k+1, \end{cases} \qquad k \in \mathbb{N}.$$

    !!! tip
        证明可通过观察真值表完成。

    @import "images/3/1/2/add_self.png"

    !!! tip
        奇数个相同项相加等于其本身，偶数个相同项相加等于 0。

    @import "images/3/1/2/add_self_many.png"

!!! tip
    逻辑运算的结果也是逻辑变量，这里的乘法和加法是逻辑变量间的一位不进位乘和一位不进位加，并非我们在现实中常见的多位有进位乘和多位有进位加。

    $$Y = (A \cdot B) \bmod 2$$

    $$Y = (A + B) \bmod 2$$

    由于逻辑变量和逻辑运算都在 $GF(2)$ 上，所以可以省略 $\bmod \ 2$。

观察上述数轴可以发现，从一个数出发，向左或向右前进相同距离的结果是一样的。

$$\cdots \xrightleftharpoons[\,-1\,]{\,+1\,} 1 \xrightleftharpoons[\,-1\,]{\,+1\,} 0 \xrightleftharpoons[\,-1\,]{\,+1\,} 1 \xrightleftharpoons[\,-1\,]{\,+1\,} 0 \xrightleftharpoons[\,-1\,]{\,+1\,} 1 \xrightleftharpoons[\,-1\,]{\,+1\,} 0 \xrightleftharpoons[\,-1\,]{\,+1\,} 1 \xrightleftharpoons[\,-1\,]{\,+1\,} \cdots$$

所以可以得出结论：

$$A + B = A - B$$

也就是说，在逻辑运算中，**加减等价**。

!!! info
    令 $A = 0$，可得出以下推论：

    $$B = -B$$

    !!! tip
        取反指非运算，并不是取相反数。

#### 3.1.3 逻辑运算律

##### 交换律、结合律、分配律

加法和乘法满足交换律：

$$A + B = B + A$$

$$A \cdot B = B \cdot A$$

!!! example
    @import "images/3/1/3/commutativity.png"

加法和乘法满足结合律：

$$A + (B + C) = (A + B) + C$$

$$A \cdot (B \cdot C) = (A \cdot B) \cdot C$$

!!! example
    @import "images/3/1/3/associativity.png"

加法不满足分配律，乘法满足分配律：

$$A + B \cdot C \neq (A + B) \cdot (A + C)$$

$$A \cdot (B + C) = A \cdot B + A \cdot C$$

!!! example
    @import "images/3/1/3/distributivity.png"

运算符 $+$、$-$、$\cdot$ 属于代数运算符，使用代数运算符连接的式子被称为代数运算式，简称代数式。相同运算符的运算次序是 **先左后右**，而不同运算符的运算次序是 **先乘法再加法**，若有括号，则 **先进行括号内运算**。

!!! example
    !!! question
        证明：任何数乘以本身的非等于 0。

        $$A \cdot \lnot A = 0$$

    !!! quote
        $$\begin{array}{lll} A \cdot \lnot A & = & A \cdot (A + 1) \\ & = & A \cdot A + A \\ & = & A + A \\ & = & 0 \end{array}$$

    @import "images/3/1/3/mul_self_not.png"

!!! example
    !!! question
        证明：
        $$A \land B = (\lnot A \oplus B) \land B$$

    !!! quote
        $$\begin{array}{lll} (\lnot A \oplus B) \land B & = & (A + 1 + B) \cdot B \\ & = & A \cdot B + B + B \cdot B \\ & = & A \cdot B + B + B \\ & = & A \cdot B\end{array}$$

    !!! tip
        有时会需要让与门上某些电线从特定逻辑灯引出，这时可以使用这个技巧重叠电线。

        @import "images/3/1/3/and_transformatio.png"

##### 普通灯

完整逻辑门由逻辑门和其上逻辑灯组成，普通灯是异或逻辑，输入是其上所有电线连接的所有电源；逻辑门的逻辑取决于类型，输入是其上所有逻辑灯。

普通灯是异或逻辑，其上电线连接 $m$ 个电源的普通灯代数式中有 $m$ 项相加，每一项都对应一个其上电线连接的电源，如果逻辑灯输入有取反则加上 1。

!!! quote
    $$\mathrm{Lamp}(S_1,\dots,S_m;s) = \sum_{i=1}^{m} S_i + s$$

    $m$ 电源输入普通灯代数式，$s$ 是逻辑灯本身状态，灭为 0，亮为 1。

!!! tip
    线异或在状态用电器发生，输入是状态用电器上全部电线连接的全部电源。

!!! example
    有时会需要让某根电线穿过双灯异或门而不干扰异或门逻辑。
    
    设异或的两个输入分别为 $M$ 和 $N$，输出为 $Y$，则：
    
    $$Y = M + N$$

    令 $M = A + B,\ N = B$ 则：

    $$Y = (A + B) + B = A$$

    @import "images/3/1/3/xor_anti-interference.png"

    $Y$ 始终等于 $A$，与 $B$ 的值无关。

!!! tip
    代入法是一种常见的代数运算方法。当某个逻辑变量已知等价于一个由其他变量构成的代数式时，可以在任意逻辑式中用该表达式直接替换原变量，而不改变逻辑结果。

    逻辑灯的输入是其上全部电线连接的全部电源状态，输出是逻辑灯状态；逻辑门输入是其上全部逻辑灯状态，输出是逻辑门状态。
    
    完整逻辑门是由逻辑门和其上逻辑灯组成的，所以将逻辑灯的代数式代入逻辑门的代数式就可以得到完整逻辑门的代数式，输入是逻辑门上逻辑灯上全部电线连接的全部电源状态，输出是逻辑门状态。

##### 与门

与门是与逻辑，其上有 $n$ 灯的与门代数式中有 $n$ 项相乘，每一项都对应一个其上普通灯，如果逻辑门输出有取反则加上 1。

!!! quote
    $$\mathrm{AndGate}(L_1,\dots,L_n;s) = \prod_{j=1}^{n} L_j + s$$

    $n$ 灯输入与门代数式，$s$ 是逻辑门本身状态，灭为 0，亮为 1。

将普通灯代数式带入与门代数式即可得到由普通灯和与门组成的完整与门的代数式。

!!! quote
    设与门上第 $j$ 个普通灯代数式如下：

    $$L_j = \mathrm{Lamp}(S_{j1},\dots,S_{jk_j};s_j)$$

    则完整与门代数式如下：

    $$\mathrm{FullAndGate} \Big(\{S_{ji}\}_{\substack{1\le j\le n\\1\le i\le k_j}}; \{s_j\}_{j=1}^{n}, s\Big) = \prod_{j=1}^{n} \left(\sum_{i=1}^{k_j} S_{ji} + s_j \right) + s$$

!!! example
    !!! question
        写出下列完整与门的代数式：

        @import "images/3/1/3/and.png"

    * $Y_1 = (A + B + 1)(A + B + C)A$

    * $Y_2 = (A + C)(A + B + C + 1)C + 1$

    * $Y_3 = (B + 1)(A + B + C + 1)(C + 1) + 1$

    * $Y_4 = B(A + B + C)(A + 1)$

如果代数式或加一后的代数式可因式分解，每一个因式里只含加法不含乘法，则其对应的逻辑可以只用一个与门实现。

!!! tip
    既代数式可以写成如下形式时，对应逻辑可以只用一个与门实现。

    $$f = \prod_{j=1}^{n} \left(\sum_{i} S_{ji} + s_j \right) \quad \text{or} \quad f+1 = \prod_{j=1}^{n} \left(\sum_{i} S_{ji} + s_j \right)$$

能只使用一个逻辑门实现的逻辑被称为 **简单逻辑**。

!!! example
    或运算逻辑式：

    $$A \lor B = \lnot (\lnot A \land \lnot B)$$

    或运算代数式：

    $$AB + A + B$$

    !!! quote
        $$\begin{array}{lll} A \lor B & = & \lnot (\lnot A \land \lnot B) \\ & = & (A + 1)(B + 1) + 1 \\ & = & AB + A + B + 1 + 1 \\ & = & AB + A + B \end{array}$$

    或运算代数式可以使用因式分解将其写成因式里只含加法的形式：

    $$\begin{array}{lll} AB + A + B & = & AB + A + B + 1 - 1 \\ & = & (A + 1)(B + 1) + 1 \end{array}$$

    所以或逻辑可以只用一个与门实现。

    !!! tip
        这里利用了推论 $1 = -1$。
    
    @import "images/3/1/3/or.png"

!!! example
    逻辑式：

    $$(A \lor B) \land (C \lor D)$$

    代数式：

    $$(AB + A + B)(CD + C + D)$$

    代数式及代数式加一都不可将因式中的乘法消除，因此不可只用一个与门表示。

    @import "images/3/1/3/or_and.png"

##### 异或门

异或门是独热逻辑，$n$ 灯异或门代数式中有 $n$ 个逻辑变量，每一个逻辑变量都对应一个其上普通灯，如果逻辑门输出有取反则加上 1。

!!! quote
    考虑三输入独热真值表：

    | > | > | 输入 | 输出 |
    | --- | --- | --- | --- |
    | A | B | C | Y |
    | 0 | 0 | 0 | 0 |
    | 0 | 0 | 1 | 1 |
    | 0 | 1 | 0 | 1 |
    | 0 | 1 | 1 | 0 |
    | 1 | 0 | 0 | 1 |
    | 1 | 0 | 1 | 0 |
    | 1 | 1 | 0 | 0 |
    | 1 | 1 | 1 | 0 |

    使用最小项之和写出逻辑式：

    $$\mathrm{OneHot}(A, B, C) = \lnot A \land \lnot B \land C \oplus \lnot A \land B \land \lnot C \oplus A \land \lnot B \land \lnot C$$

    转换为代数式：

    $$\begin{array}{lll} \mathrm{OneHot}(A, B, C) & = & (A + 1)(B + 1)C + (A + 1)B(C + 1) + A(B + 1)(C + 1) \\ & = & (AB + A + B + 1)C + \\ & & (AC + A + C + 1)B + \\ & & (BC + B + C + 1)A \\ & = & ABC + AC + BC + C + \\ & & ABC + AB + BC + B + \\ & & ABC + AB + AC + A \\ & = & ABC + A + B + C\end{array}$$

    !!! tip
        这里利用了推论 $A + A = 0$，出现奇数次的项被保留，偶数次的项被消掉。

    同理四输入独热的表达式为：

    $$\mathrm{OneHot}(A, B, C, D) = ABC + ABD + ACD + BCD + A + B + C + D$$

    !!! tip
        证明留给读者进行，同样是奇数次的项被保留，偶数次的项被消掉。

!!! quote
    由上述结论推广可得：

    $$\mathrm{XorGate}(L_1,\dots,L_n; s) = \sum_{\substack{I \subseteq \{1,\dots,n\} \\ |I| \equiv 1 \pmod{2}}} \; \prod_{i \in I} L_i + s$$

    $n$ 灯输入异或门代数式，$s$ 是逻辑门本身状态，灭为 0，亮为 1。

将普通灯代数式带入异或门代数式即可得到由普通灯和异或门组成的完整异或门的代数式。

!!! quote
    设异或门上第 $j$ 个普通灯代数式如下：

    $$L_j = \mathrm{Lamp}(S_{j1},\dots,S_{jk_j};s_j)$$

    则完整异或门代数式如下：

    $$\mathrm{FullXorGate} \Big(\{S_{ji}\}_{\substack{1\le j\le n\\1\le i\le k_j}}; \{s_j\}_{j=1}^{n}, s\Big) \\ =  \sum_{\substack{I \subseteq \{1,\dots,n\} \\ |I| \equiv 1 \pmod{2}}} \; \prod_{i \in I} \left(\sum_{i=1}^{k_j} S_{ji} + s_j \right) + s$$

!!! tip
    同理，如果代数式可以写成如下形式时，对应逻辑可以只用一个异或门实现。

    $$f = \sum_{\substack{I \subseteq \{1,\dots,n\} \\ |I| \equiv 1 \pmod{2}}} \; \prod_{i \in I} \left(\sum_{i=1}^{k_j} S_{ji} + s_j \right) + s \\ \text{or} \\ f+1 = \sum_{\substack{I \subseteq \{1,\dots,n\} \\ |I| \equiv 1 \pmod{2}}} \; \prod_{i \in I} \left(\sum_{i=1}^{k_j} S_{ji} + s_j \right) + s$$

!!! example
    观察下方电路：

    @import "images/3/1/3/xor_to_and.png"

    写出代数式为：

    $$(ABC + A + B + C) + A + B + C = ABC$$

    满足与逻辑。

    观察下方电路：

    @import "images/3/1/3/and_to_xor.png"

    写出代数式为：

    $$(ABC) + A + B + C = ABC + A + B + C$$ 

    满足独热逻辑。

    可见可以用与门实现异或门的独热逻辑，也可以用异或门实现与门的与逻辑。

!!! example
    三灯异或门的代数式为：

    $$F = ABC + A + B + C$$

    令逻辑灯 $A = X + Y,\ B = X + Y,\ C = Y$，则：

    $$F = (X + Y)(X + Y)Y + (X + Y) + (X + Y) + Y = XY$$

    满足二输入与逻辑。

    @import "images/3/1/3/3_xor_to_2_and.png"

!!! example
    三灯异或门的代数式为：

    $$F = ABC + A + B + C$$

    令逻辑灯 $A = X + 1,\ B = Y + 1,\ C = 1$，则：

    $$F = (X + 1)(Y + 1)1 + (X + 1) + (Y + 1) + 1 = XY$$

    满足二输入与逻辑。

    @import "images/3/1/3/3_xor_to_2_and_2.png"

!!! info
    易证：

    $$\mathrm{OneHot}(0, A_1, A_2, \cdots, A_n) = \mathrm{OneHot}(A_1, A_2, \cdots, A_n)$$

    $$\mathrm{OneHot}(1, A_1, A_2, \cdots, A_n) = \lnot A_1 \land \lnot A_2 \land \cdots \land \lnot A_n$$

!!! example
    三灯异或门的代数式为：

    $$F = ABC + A + B + C$$

    令逻辑灯 $A = X,\ B = Y,\ C = 1,\ Z = F + 1$，则：

    $$Z = (XY1 + X + Y + 1) + 1 = XY + X + Y$$
    
    满足二输入或逻辑。

    @import "images/3/1/3/3_xor_to_2_or.png"

#### 3.1.4 最小项

