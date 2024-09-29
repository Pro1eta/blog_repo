---
title: 命题逻辑 
published: 2024-03-09
description: 主要介绍了命题逻辑, 逻辑运算符, 真值表, 命题等价式, 范式等
tags: [逻辑, 离散数学]
categories: 课程笔记
draft: false
---



# 前言

这是离散数学的笔记, 我打算仅做数理逻辑部分, 其内容是基于教师讲义以及教材.:smile:

我用的教材[^1], 以及最后的考试都是英文, 出于这个考虑, 这些笔记大概会用英文写成, 里面也会掺中文, 主要是因为~~英语很烂~~方便对照. 当然, 还有一个原因是教材关于数理逻辑这部分的内容比较浅显, 不得不用中文补充一些进来. 你会发现后面几篇笔记中文含量越来越大, 笔记篇幅越来越少, 主要是因为我变懒了XD.

# 命题逻辑

***Propositional Logic***

## 命题

***Proposition*** 

>***Definition*** 
>
>**proposition 命题**
>
>- a statement(i.e. a declarative sentence) - with some definite meaning, (not vague or ambiguous).
>- having a truth value that is either true of false, but not both.

- **Atoms** **原子命题**: formula with no deeper propositional structure, that is, a formula that contains no logical connectives or equivalently a formula that has no strict subformulas.
- **Compound propositions** **复合命题**: build up from atoms using operators.

if $p \to q$, then

- $p \to q$ is the **converse(逆命题)** of it.
- $\neg q \to \neg p$ is the **contrapositive(逆否命题)** of it.
- $\neg p \to \neg q$​ is the **inverse(否命题)** of it. 

>***Definition***
>
>**formula (命题)公式**
>
>- All atomes are formulas.
>- If $p$ is a formula, then $\neg p$ is a formula.
>- If $p$ and $q$ is a formula, then the following are formulas: $p \land q$  $p\lor q$  $p \oplus q$  $p \to q$  $p \leftrightarrow q$ e.g.

## 命题变量

***Propositional variables***

We use letters to denote propositional variables (or statement variables).The conventional letters used for propositional variables are p, q, r, s, ...

## 逻辑运算符

***Operators / Connectives***

An operator or connective combines n operand expressions into a larger expression. **Unary** operators take 1 operand while **binary** operators take 2 operands.

|       Formal Name       | Nickname | Arity  |      Symbol       |
| :---------------------: | :------: | :----: | :---------------: |
|    Negation operator    |   NOT    | Unary  |      $\neg$       |
|  Conjunction operator   |   AND    | Binary |      $\land$      |
|  Disjunction operator   |    OR    | Binary |      $\lor$       |
| Exclusive - OR operator |   XOR    | Binary |     $\oplus$      |
|  Implication operator   | IMPLIES  | Binary |       $\to$       |
| Biconditional operator  |   IFF    | Binary | $\leftrightarrow$ |

### 否定, 非

***The Negation Operator***

The unary negation operator transforms a prop. into its negation.

>***E.g.***
>
>if $p=$ "I have brown hair."
>
>then $\neg p=$ "I do **not** have brown hair."



### 合取, 与

***The Conjunction Operator***

The binary conjunction operator "$\land$"(AND) combines two propositions to form their logical conjunction. 

- **In fact, $\neg$ and $\land$ are sufficient to express any Boolean truth table.**

### 析取, 或

***The Disjunction Operator***

The binary disjunction operator "$\lor$"(OR) conbines two prop. to form their logical disjunction.



### 异或

***The Exclusive-or Operator***

The binary exclusive-or operator "$\oplus$"(XOR) combines two propositions to form their logical "exlusive or".

>***E.g.***
>
>$p=$ "I will earn an A in this course,"
>
>$q=$ "I will either earn an A in this course,"
>
>$p \oplus q=$ "I will either earn an A in this course, or I will drop it(**but not both**)."

"Or" in English can be ambiguous regarding the "**both**" case.



### 蕴涵

***The Implication Operator***

The implication $p \to q$ states that $p$ implies $q$.

*I.e.* If $p$ is true then $q$ is true. However, if $p$ is **not** true, then q could be either true or false.  

- $p \to q$ is flase **only** when $p$ is true but $q$ is false.
- $p \to q$ does not mean that $p$ causes $q$.

#### Different Ways of Expressing $p \to q$

- $p$ implies $q$ 

- if $p$, then $q$

- if $p$, $q$
- when $p$, $q$

- whenever $p$, $q$

- $q$ if $p$

- $q$ when $p$

- $q$ whenever $p$

- $p$ only if $q$
- $q$ is necessary for $p$
- $q$ follows from $p$
- $q$ is implied by $p$
- $q$ unless $\neg p$​



### 同或, 逻辑等价

***The Biconditional Operator*** 

The biconditional $p \leftrightarrow q$ states that $p$ is true **if and only if** q is true.

### 真值表汇总

***The Truth Table of Boolean Operations***

| $p$  | $q$  | $\neg p$ | $p \land q$ | $p\lor q$ | $p \oplus q$ | $p \to q$ | $p \leftrightarrow q$ |
| ---- | :--: | :------: | :---------: | :-------: | :----------: | :-------: | :-------------------: |
| F    |  F   |    T     |      F      |     F     |      F       |     T     |           T           |
| F    |  T   |    T     |      F      |     T     |      T       |     T     |           F           |
| T    |  F   |    F     |      F      |     T     |      T       |     F     |           F           |
| T    |  T   |    F     |      T      |     T     |      F       |     T     |           T           |

Besides, we have two more operators.

### 与非

***NAND***

The proposition $p \ N\!A\!N\!D \ q$ is true when either $p$ or $q$, or both, are false;and it is false when both $p$ and $q$ are true.

$p \ N\!A\!N\!D \ q$ is denoted by $p \ | \ q$.

### 或非

***NOR***

The proposition $p \ N\!O\!R \ q$ is true when both $p$ and $q$ are false, and it is false otherwise.

$p \ N\!O\!R \ q$ is denoted by $p\downarrow q$.



### 优先级

***Precedence of Logical Operators***

- It's important to use **parenthesis** to group sub-expressions

|     operator      | Predence |
| :---------------: | :------: |
|      $\neg$       |    1     |
|      $\land$      |    2     |
|      $\lor$       |    3     |
|       $\to$       |    4     |
| $\leftrightarrow$ |    5     |



### 一致系统规范说明

***Consistent System Specifications***

>***Definition***
>
>**Consistent System Specifications 一致系统规范说明**
>
>- A list of propositions is **consistent** if it is possible to assign truth values to the proposition variables so that each proposition is true.
>
>系统规范说明是**一致的**, 如果可以为所有的**命题变量**设定真值, 使得命题变量构成的每一个**命题**均为**真**.



>***E.g.***
>
>Let $p$:“The diagnostic message is stored in the buffer.”
>
>设 $p$: 诊断信息被存储在缓冲区中.
>
>$q$: “The diagnostic message is retransmitted.”
>
>$q$: 诊断信息被重新发送.
>
>
>
>for $p\lor q$, $p \to q$, $\neg p$,
>
>If $p$ is flase while $q$ is true, then all three prop. are true, so **the specification is consistent**.

---

# 命题等价式

***Propositional Equivalences*** 

>***Definition*** 
>
>**Tautology, contradiction, contingency** 
>
>**永真式, 永假式, 可能式**
>
>- A compound proposition that is always true, no matter what the truth values of the propositional variables that occur in it, is called a **tautology(永真式, 或者重言式)**.
>
>- A compound proposition that is always false is called a **contradiction(永假式, 或者矛盾式)**.
>
>- A compound proposition that is neither a tautology nor a contradiction is called a **contingency(可能式)**



>**Rule of substitution** **置换规则**
>
>Suppose $P$ is a tautology, if $p$ is a primitive statement in $P$ and we can replace $p$ with the statement $q$, then the new statement $P'$ is also a tautology.
>
>在一个永真公式中, 任何一个命题变元 $R$ 出现的每一处, 用另一个命题公式代入, 所得命题公式仍然是永真式.



>**Rule of replacement** **代入规则**
>
>Within the context of a logical proof, logically equivalent expressions may replace each other.
>
>给定公式 $A$, 其所有子公式为 $a_1,a_2,\dots,a_n$, 设 $a_i \equiv b_i$, 用 $b_i$ 替换 $a_i$, 所得公式为 $B$, 则 $A \equiv B$.

## 逻辑等价式

***Logical Equibalences***

>***Definition*** 
>
>**Logical Equibalences 逻辑等价式**
>
>Compound propositions that **have the same truth values in all possible cases** are called **logically equivalent**. The notation
>$$
>p \equiv  q
>$$
>or
>$$
>p \Leftrightarrow q
>$$
>donates that $p$ and $q$ are **logically equivalences**.

- **tips**: We will also say: they express **the same truth function** or the same function from values for atoms to values for the whole formula.In other words, two syntactically compound propositions may be semantically identical.
- **tips**: The symbol $\equiv$ is **NOT** a logical connective, and $p \equiv  q$ is not a compound proposition but rather is the statement that $p \leftrightarrow q$ is a tautology.

## 等价规则

***Equivalences***



To shorten the length, let's make $\mathbf{T}$ short for **tautology** and $\mathbf{F}$ for **contradiction**. There's some logical equivalences.

| *Equivalence*                                           | *Name*                              |
| ------------------------------------------------------- | ----------------------------------- |
| $p \land \mathbf{T} \equiv p$                           | Identity laws<br />同一律           |
| $p \lor \mathbf{F} \equiv p$                            | Identity laws<br />同一律           |
| $p \lor \mathbf{T} \equiv \mathbf{T}$                   | Domination laws<br />零律, 支配律   |
| $p \land \mathbf{F} \equiv \mathbf{F}$                  | Domination laws<br />零律, 支配律   |
| $p \land p \equiv p$                                    | Idempotent laws<br />等幂律         |
| $p \lor p \equiv p$                                     | Idempotent laws<br />等幂律         |
| $\neg (\neg)p \equiv p$                                 | Double negation law<br />双重否定律 |
| $p \land q \equiv q \land p$                            | Commutativive laws<br />交换律      |
| $p \lor q \equiv q \lor p$                              | Commutativive laws<br />交换律      |
| $(p \lor q) \lor r\equiv q \lor (p \lor r)$             | Associative laws<br />结合律        |
| $(p \lor q) \land r\equiv (p \lor q) \land (p \lor r)$  | Distributive laws<br />分配律       |
| $(p \land q) \lor r\equiv (p \land q) \lor (p \land r)$ | Distributive laws<br />分配律       |
| $\neg(p \land q) \equiv \neg q \lor\neg p$              | De Morgan's laws<br />德·摩根律     |
| $\neg(p \lor q) \equiv \neg q \land\neg p$              | De Morgan's laws<br />德·摩根律     |
| $p \lor (p \land q ) \equiv p$                          | Absorption laws<br />吸收律         |
| $p \land (p \lor q ) \equiv p$                          | Absorption laws<br />吸收律         |
| $p \lor  \neg p\equiv \mathbf{T}$                       | Tautology<br />排中律               |
| $p \land \neg p\equiv \mathbf{F}$                       | Contradiction<br />矛盾律           |
| $p \to q \equiv \neg p \lor q$                          | Implication<br />蕴涵等价式         |
| $(p \to q) \land (q \to p) \equiv p \leftrightarrow q$  | 同或等价式                          |
| $(p \to q) \land (p \to \neg q) \equiv \neg p$          | Absurdity<br />归谬                 |
| $p \to q \equiv \neg q \to \neg p$                      | Contrapositive<br />蕴涵逆反式      |
| $p \land q \to r \equiv p \to (q\to r)$                 | Exportation<br />输出律             |
| $p \to q \equiv \neg q \to \neg p$                      | 假言易位                            |

| Logical Equivalences Involving Conditional Statements |
| ----------------------------------------------------- |
| $p \land q \equiv \neg (p \to \neg q)$                |
| $p \lor q \equiv \neg p \to q$                        |
| $\neg (p \to q) \equiv p \land \neg q$                |
| $(p \to q) \land (p \to r) \equiv p \to (q \land r)$  |
| $(p \to r) \land (q \to r) \equiv (p \lor q) \to r$   |
| $(p \to q) \lor (p \to r) \equiv p \to (q \lor r)$    |
| $(p \to r) \lor (q \to r) \equiv (p \land q) \to r$   |

| Logical Equivalences Involving Biconditional Statements      |
| ------------------------------------------------------------ |
| $p \leftrightarrow q \equiv (p \to q) \land (q \to p)$       |
| $p \leftrightarrow q \equiv \neg p \leftrightarrow \neg q$   |
| $p \leftrightarrow q \equiv (p \land q) \lor (\neg p \land \neg q)$ |
| $\neg (p \leftrightarrow q) \equiv p \leftrightarrow \neg q$ |



## 范式的存在性定理

这一部分用中文写, 因为原教材和百科中基本没有对这一段的提及, 或者百科内容与教师讲授内容与原教材内容不一致. 出于这些原因用中文较好.

>***Definition***
>
>**基本和(子句)**
>
>由有限个命题变量或其否定析取, 构成的析取式, 称为**基本和**, 或者**(简单)析取式**.



>***Definition***
>
>**基本积**
>
>由有限个命题变量或其否定合取, 构成的合取式, 称为**基本积**, 或者**(简单)合取式**.



>***E.g.***
>$\neg p \lor q \lor p \lor r$​ 是**简单析取式**.

**tips**: 一个变量本身可以看作基本和或者基本积.

然后, 引入析取范式与合取范式.

>***Definition***
>
>**析取范式(disjunctive normal form, or DNF)**
>
>A logical formula is considered to be in DNF if it is a disjunction of one or more conjunctions of one or more **literals**.
>
>由有限个简单合取式(基本积)析取,构成的析取式, 称为**析取范式**.



>***Definition***
>
>**合取范式(consjunctive normal form, or CNF)**
>
>A formula is in CNF if it is a conjunction of one or more clauses, where a clause is a disjunction of **literal**s.
>
>由有限个简单析取式(基本和)合取, 构成的合取式, 称为**合取范式**.

**tips**: Let's add a concept: 

>A **literal** is an atomic formula (also known as an atom or prime formula) or its negation. 
>
>**文字**是一个原子命题或者它的否定.

"简单析取式"和"简单合取式"这两个概念没有在百科找到. 这两个概念的作用似乎只是为了定义DNF和CNF. 与"基本和", "基本积"相似的概念可以参见[***子句（clause）- Wikipedia***](https://en.wikipedia.org/wiki/Clause_(logic))和 [***Product term - Wikipedia***](https://en.wikipedia.org/wiki/Product_term).

>***Theorem***
>
>**范式存在定理**
>
>Any Boolean function has a CNF, and a DNF form.
>
>任意的命题公式均存在一个与之等值的析取范式和合取范式.

The proof is very trivial.

**tips**: 析取范式和合取范式不唯一.



## 主范式

***Principal Normal Form***

### 极小项, 极大项

***Minterm and Maxterm***

>***Definition***
>
>**Minterm ** **极小项**
>
>For a boolean function of $n$ variables $x_1,x_2,\dots,x_n$, a product term in which each of the $n$​ variables appears once (either in its complemented or uncomplemented form) and appears in order is called a **minterm**.
>
>设简单合取式中有 $n$ 个命题变量 $x_1,x_2,\dots,x_n$, 每个文字都出现, 并且仅出现一次, 这样的公式称为**极小项**.

- **indexing minterm** **极小项的编码**

  Minterms are often numbered by a binary encoding of the complementation pattern of the variables, where the variables are written in a standard order, usually alphabetical.

  极小项的命题变量的常常按下标排列(或者字典序列排列).

  若给变量 $x_i$ 赋值二进制值 $1$, 给 $\neg x_i$ 赋值二进制值 $0$, 那么可以给出一个 $n$ 位二进制编码来表示极小项, 比如可以记作 $m_{101\dots}$. 

  > ***E.g.*** we can notate minterm just like:
  >
  > $m_0 = m_{00 \dots00}=\neg p_1 \land \neg p_2 \land \cdots \land \neg p_n$​​
  >
  > $m_3 = m_{0 \dots011}=\neg p_1 \land \neg p_2 \land \cdots \land  \neg p_{n-2} \land p_{n-1} \land p_n$

  显然, 极小式的下标值(十进制)为:

$$
\sum_{i=1}^{n}2^{i-1}value(x_i)
$$

- **极小项的性质**
  1. 每一个**极小项**, 当其赋值与编码相同的时候, 真值为 $\mathbf{T}$, 否则一定为 $\mathbf{F}$.
  2. 任意**不同**极小项的**合取永假**.
  3. **所有极小项**的**析取永真**.
  4. 没有两个极小项是等价的.

>***Definition***
>
>**Maxterm** **极大项**
>
>For a boolean function of $n$ variables $x_1,x_2,\dots,x_n$, a sum term or clause in which each of the $n$ variables appears once (either in its complemented or uncomplemented form) is called a **maxterm**.
>
>设简单析取式中有 $n$ 个命题变量 $x_1,x_2,\dots,x_n$, 每个文字都出现, 并且仅出现一次, 这样的公式称为**极大项**.

- **indexing Maxterm** **极大项的编码**
  类似地, 极大项也可以编码, 规则与极小项基本一致. 不同的是将 $p_i$ 记为 $0$, 将 $\neg p_i$ 记为 $1$. 极大项的记法与极小项完全一致.

- **极大项的性质**
  1. 每一个**极大项**, 当其赋值与编码相同的时候, 真值为 $\mathbf{F}$, 否则一定为 $\mathbf{T}$​.
  2. 任意**不同**极大项的**析取永真**.
  3. **所有极大项**的**合取永假**.
  4. 没有两个极大项是等价的.

### 主析取范式, 主合取范式

***Principal Disjunctive Form and Conjunctive Normal Form***



Now it's time for our main characters to come on stage!

>***Definition***
>
>**Principal disjunctive normal form or PDNF**
>
>**主析取范式**
>
>A formula is in principal disjunctive normal form if it is a disjunction of minterns.
>
>若干个不同的极小项的析取式, 称为**主析取范式**.



>***Definition***
>
>**Principal conjunctive normal form or PCNF**
>
>**主合取范式**
>
>A formula is in principal disjunctive normal form if it is a conjunction of maxterns.
>
>若干个不同的极大项的合取式, 称为**主合取范式**.



>***Theorem***
>
>任何一个公式均存在一个与之等值的**主析取范式**, 而且是**唯一**的.
>
>任何一个公式均存在一个与之等值的**主合取范式**, 而且是**唯一**的.

The proof is very trivial.

**tips**: 不难发现, **永假式(controdiction)**的主合取范式含有 $\dots\land p \land \cdots \land\neg p$ 这样的因子. 而**永真式(Tautology)**的主合取范式 $\dots\lor p \lor \cdots \lor\neg p$ 这样的因子.

### 求取主范式

***Find The Principal Form***



主要有两种方法.

#### 真值表法

***Using the truth table***



- 主析取范式
  简而言之, 跟据公式的真值表, 找出能够使公式为**真**的赋值, 写出对应的极小项, 然后将它们析取而成即可.
- 主合取范式
  跟据公式的真值表, 找出能够使公式为**假**的赋值, 写出对应的极大项, 然后将它们合取而成即可.

这样做的主要依据是极小项和极大项的性质, 以及主范式的唯一性.





#### 等值演算

***Equivalence***



对于求取**主析取范式(PDNF)**, 主要是以下步骤:

1. 利用**逻辑等价式**, 将逻辑运算符全部转化为 $\neg, \land, \lor$.
2. 利用**De Morgan's laws**, 将所有 $\neg$ 转移至单个命题变量之前.
3. 将命题公式转化为析取范式, 例如 $P_1 \land P_2 \land P_3 \land \cdots \land P_n$ 的形式, 注意其中的 $P_i$ 是简单合取式, 即仅由**文字(literal)**合取而成. 
4. 设 $P_i = p_{i1} \lor p_{i2} \lor \cdots \lor p_{im}$, 其中 $p_{ij}$ 是**文字(literal)**, 如果某项重复, 利用**交换律**抵消即可; 如果缺少某一项(设为 $p_{ik}$), 可以在 $P_i$ 中合取 $p_{ik} \lor \neg p_{ik}$ 这一**重言式(tautology)**, 再利用**分配律**展开即可(若求取**主合取范式(PCNF)**, 则析取 $p_{ik} \land \neg p_{ik}$)
5. 合并重复的极小项.

>***E.g.***
>
>(等待补充)



对于求取**主合取范式(PCNF)**, 类比即可, 不赘述.

---

## 可满足性

***Satisfiability***

> A compound proposition is **satisfiable** if there is an assignment of truth values to its variables that makes it true (that is, when it is a tautology or a contingency). When no such assignments exists, that is, when the compound proposition is false for all assignments of truth values to its variables, the compound proposition is **unsatisfiable**.
>
> 复合命题是**可满足的**, 如果能够对其所有命题变量赋真值, 使得原复合命题为真.(换句话说, 这个复合命题是重言式或可能式). 若所有真值赋值的情况下, 复合命题均为假, 则是**不可满足的**.

### $n$ 皇后问题

***The $n$​-Queens Problem***

### 数独

***Sudoku***

(等待补充~~我会补充的, 信我~~)



[^1]: Kenneth H. Rosen.Discrete Mathematics and Its Applications.离散数学及其应用.Eighth edition.

