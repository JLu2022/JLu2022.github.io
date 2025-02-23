对Policy Gradient Methods for Reinforcement Learning with Function Approximation中的数学公式进行推导

先交代必要的数学符号
$P_{ss'}^{a}=Pr \{s_{t+1}=s|s_{t}=s,a_{t}=a\}$即状态转移方程.
$R_{s}^{a}=\mathbb{E}\{r_{t+1}|s_t=s,a_t=a\}$

文中谈到了两类优化问题：

1. 无折扣平均奖励的情况
$$\begin{equation}
\rho(\pi)=\underset{n\rightarrow\infty}{lim}\sum_{t=1}^{n}(r_{t}|\pi)=\sum_{s}d^{\pi}(s)\sum_{a}\pi(s,a)R_{s}^{a} 
\end{equation}$$
注意在平均奖励的情况下，后面跟着的不是Q而是单步奖励R

其中$d^{\pi}(s)=\underset{t\rightarrow\infty}{lim}Pr\{s_{t}=s|s_0,\pi\}$

而$Q^{\pi}(s,a)=\underset{t\rightarrow\infty}{lim}\mathbb\{r_t-\rho(\pi)|s_0=s,a_0=a,\pi\}$

# Theorem 1 策略梯度定理
$\nabla_{\theta}\rho=\sum_{s}d^{\pi}(s)\sum_{a}\nabla_{\theta}\pi(s,a)Q^{\pi}(s,a)$

意义：对无折扣平均奖励来说，梯度的方向是策略参数梯度的方向。

# Proof of Theorem 1
由式(1)入手，

$$
\begin{aligned}
    \nabla_{\theta}\rho(\pi)&=\nabla_{\theta}\sum_{s}d^{\pi}(s)\sum_{a}\pi(s,a)R_{s}^{a}\\
                            &=\sum_{s}[\nabla_{\theta}d^{\pi}(s)]\sum_{a}\pi(s,a)R_{s}^{a}+\sum_{s}d^{\pi}(s)\sum_{a}[\nabla_{\theta}\pi(s,a)]R_{s}^{a}\\
                            &=\sum_{s}d^{\pi}(s)\sum_{a}[\nabla_{\theta}\pi(s,a)]R_{s}^{a}&&(根据归一化条件， 有\sum_{s}d^{\pi}(s)=1;则\sum_{s}[\nabla_{\theta}d^{\pi}(s)]=\nabla_{\theta}\sum_{s}[d^{\pi}(s)]=0;而尽管\sum_{a}\pi也可以满足归一化条件，但是后面跟着一个R，而使其不能为1了，因为导数运算能穿越求和但是不能穿过互相依赖的R和\pi)\\
\end{aligned}
$$
可以看到此时的结构已经非常接近我们的目标了，但是最后一项还是不一样，因此，我们要进一步证明:
$\sum_{a}\pi(s,a)R_{s}^{a}-\sum_{a}\pi(s,a)Q^{\pi}(s,a)=某个常数$

在平均奖励设定下，为了避免无限时间累加的问题，引入差分值函数$h^{\pi}(s)=\mathbb{E}_{\pi}[\sum_{t=0}^{\infty}(r(s_t,a_t)-\rho)|s_0=s]$和差分Q函数$Q^{\pi}(s,a)=r(s,a)-\rho+\sum_{s'}P_{ss'}^{a}h^{\pi}(s')$

Bellman 方程的一般形式:
$V^{\pi}=\mathbb{E}_{a\sim\pi(a|s)}[r(s,a)+\gamma\sum_{s'}P_{ss'}^{a}V^{\pi}(s')]$
Bellman方程的差分形式（只适用于平均奖励RL而不是折扣奖励RL）：
$\lambda+V^{\pi}=\sum_{a}\pi(a|s)[r(s,a)+\sum_{s'}P_{ss'}^{a}V^{\pi}(s')]$



