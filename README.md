# An Introduction to signal Detection and Estimation
 BUPT homework

## HW-1

### 1st problem

![image-20210814181020927](README.assets/image-20210814181020927.png)

#### solution (a):

Firstly, according to $(II.B.10)$​, write the likelihood ratio as:
$$
\begin{aligned}
L(y)&=\frac{p_1(y)}{p_0(y)}\\
&=\begin{cases}
\frac{3}{2(y+1)}, & 0\leq y \leq 1\\
meaninglesss, & \text{otherwise}
\end{cases}
\end{aligned}
$$


according to $(II.B.12)$​ The bayes rule can be writen as:
$$
\delta_{B}(y)= \begin{cases}1 & \text { if } L(y) \geq \tau \\ 0 & \text { if } L(y)<\tau\end{cases}
$$
where $\tau = 1$​ under the uniform costs and equal priors,

The plot of $L(y)$​ and $\tau$ is drawing as :

<img src="README.assets/image-20210814190000805.png" alt="image-20210814190000805" style="zoom:50%;" />

 Thus the bayes rule is rewritten to the form as:
$$
\begin{aligned}
\delta_{B}(y)&= \begin{cases}1, \text { if }\frac{3}{2(y+1)} \geq 1 \\ 0 & \text { if } \frac{3}{2(y+1)}<1\end{cases}\\
&=\begin{cases}1 & \text { if } y \leq 0.5 \\ 0 & \text { if } y>0.5\end{cases}
\end{aligned}
$$

The bayes risk is given by $(II.B.14)$​, and  because the uniform costs and equal priors, the Bayes risk can be written as:
$$
\begin{aligned}
r(\delta_B)&=\pi_{0} P_{0}\left(\Gamma_{1}\right)+\pi_{1} P_{1}\left(\Gamma_{0}\right)\\
&=0.5\int_{0}^{0.5}p_0(y)+0.5\int_{0.5}^{1}p_1(y)
\end{aligned}
$$
Where $p(y)= 0.5\cdot(p_1(y)+p_0(y))=\frac{2y+5}{6}$​​ , the risk is rewritten as:

$$
\begin{aligned}
r(\delta_B)
= 0.5\cdot \left[\int_0^{0.5}2/3\cdot (y+1)+\int_{0.5}^{1}1 \right]
\end{aligned}
$$
```matlab
fun1 = @(y) (2/3)./(y+1);
q1 = integral(fun1, 0, 0.5)

fun2 = @(y) y.^0
q2 = integral(fun2, 0.5, 1)

fanal = 0.5*(q1+q2)
```
var the matlab code shown above, the Bayes risk is calculated as:
$$
r(\delta_B) = 0.3852
$$

#### Solution(b):

The function $ V$ Is given by :
$$
V(\pi_0) = 
\begin{cases}
\pi_0, &0 \leq \pi_0 < 3/7
\\
\pi_0\left(\int_0^{\tau^{'}} \frac{2}{3}(y+1)\cdot dy\right)+(1-\pi_0)\left(\int_{\tau^{'}}^11\cdot dy \right), &3/7 \leq \pi_0 < 3/5\\
1-\pi_0, & 3/5 \leq \pi_0 < 1
\end{cases}
$$
Where $\tau^{'}= \frac{3-5\pi_0}{2\pi_0}$ Is the threotle. Since $V(0) = 0, V(1) = 0$​, the least favorable prior $\pi_L$

 is in the interior $(0, 1)$ in this case. And it is unnecessary to consider teh case that $P_{0}(L(Y)=\tau)=P_{1}(L(Y)=\tau)=0$ since $L(Y)$​ is a continuous random variable. So an equalizer rule is found by solving:
$$
\int_0^{\tau^{'}} \frac{2}{3}(y+1)\cdot dy=\int_{\tau^{'}}^11\cdot dy 
$$
Then, $\tau_L^{'}= \frac{-5+\sqrt{37}}{2}$​​​​​, so $\pi^{'}_L = \frac{3}{2\tau_0+5}=\frac{3}{\sqrt{37}}$​​​​, so the minimax rule is:
$$
\delta_{\pi_L}(y)&= \begin{cases}1, &\text { if }y  \leq \frac{3}{\sqrt{37}} \\ 0, & \text { if } y > \frac{3}{\sqrt{37}}\end{cases}
$$
Then the minimax risk for the uniform costs is:
$$
r_u(\delta_{\pi})=0.5\cdot \int_{0}^{\frac{3}{\sqrt{37}}}2/3\cdot (y+1)+0.5\cdot \int_{\frac{3}{\sqrt{37}}}^{1}1\cdot dy=0.4099
$$

```matlab
fun1 = @(y) 1/3.*(y+1);
q1 = integral(fun1, 0, 3/sqrt(37))

fun2 = @(y) 0.5*y.^0;
q2 = integral(fun2, 3/sqrt(37), 1)

fanal = q1+q1
```



#### Solution (c):

First, write the false-alarm probability as:
$$
\begin{aligned}
P_0(p_1(Y)>\eta \cdot p_0(Y))&=P_0(L(Y)>\eta)\\
&=P_0(Y<\eta^{'})\\
&=\frac{1}{3}{\eta^{'}}^{2}+\frac{2}{3}\eta^{'}
\end{aligned}
$$
Where $\eta^{'}=\frac{3-2\eta}{2\eta}$ and get the $\eta_0^{'}$ by sovling $P_0(p_1(Y)>\eta \cdot p_0(Y))=\alpha$:
$$
\eta_0^{'} = \sqrt{1+3\alpha}-1
$$
Then the Neyman-Pearson rule is given by:
$$
\tilde{\delta}_{N P}(y)= \begin{cases}1 & \text { if } y \geq \eta_{0}^{\prime} \\ 0 & \text { if } y<\eta_{0}^{\prime}\end{cases}
$$
Where $\eta_0^{'} = \sqrt{1+3\alpha}-1$​.



### 2rd problem

![image-20210814191417390](README.assets/image-20210814191417390.png)

#### solution:

Firstly, written the likelihood ratio as:
$$
\begin{aligned}
L(y) &= \frac{p_1(y)}{p_0(y)}, \quad y\geq 0\\
&=\sqrt{2 / \pi} e^{-y^{2} / 2 +y}
\end{aligned}
$$
Then the Threshold $\tau = \frac{\pi_0}{\pi_1}$, so the $\Gamma_1 $ Can be found by:
$$
\begin{aligned}
&L(y)\geq \tau\\
\Rightarrow & \sqrt{2 / \pi} e^{-y^{2} / 2 +y}\geq\frac{\pi_0}{(1-\pi_0)}\\
\Rightarrow & y^2 -2y+2\cdot ln\left( \sqrt{\frac{\pi}{2} }\cdot \frac{\pi_0}{1-\pi_0} \right) \leq 0
\end{aligned}
$$

Then the final bayes rule under $\forall \pi_0 \in [0,1]$ can be obtained as follows:
$$
\delta_B(y)=\begin{cases} 
 1,\quad & y \in [1-\sqrt{1-c}, 1+\sqrt{1-c}] \\
 0, \quad & y \in [0, 1-\sqrt{1-c}) \cup(1-\sqrt{1-c}, +\infin)
\end{cases}
\quad
when\quad \pi_0 \in [0, \frac{1}{\sqrt{\frac{\pi}{2e}}+1} )
$$

Where $c = 2\cdot ln(\sqrt{\frac{\pi}{2}}\cdot\frac{\pi_0}{1-\pi_0})$
$$
\delta_B(y)=0
\quad
when\quad \pi_0 \in [\frac{1}{\sqrt{\frac{\pi}{2e}}+1},  +\infin)
$$


### 3rd problem



![image-20210814203115632](README.assets/image-20210814203115632.png)

#### solution （a）：

write the $pdf$ of $H_0$ and $H_1$:
$$
\begin{aligned}
p_0(y) = p(y) = e^{-y}, \quad y\in(0,+\infin)
\end{aligned}
$$
And for $H_1$
$$
p_1(y) = \int_{-\infty}^{\infty} p(y-s) p(y) d s=\int_{0}^{y} e^{s-y} e^{-s} d s=y e^{-y}, \quad y\in (0, +\infin)
$$
Thus, the likelihood ratio is:
$$
L(y)=\frac{p_{1}(y)}{p_{0}(y)}=y, \quad y>0
$$
The plot of the pdf and the likelihood ratio is :

<img src="README.assets/image-20210816122312714.png" alt="image-20210816122312714" style="zoom:50%;" />

#### Solution (b):

First, write the false-alarm probability as:
$$
\begin{aligned}
P_0(p_1(Y)>\eta \cdot p_0(Y))&=P_0(L(Y)>\eta)\\
&=P_0(Y>\eta)\\
&=\int_0^{\eta}e^{-y}\cdot dy=e^{-\eta}
\end{aligned}
$$
Then the threshold $\eta$ Can be obtained by:
$$
P_F(\delta_{NP})&=e^{-\eta}=\alpha \\
\Longrightarrow &\eta = -ln(\alpha)
$$
So the detection probability is :
$$
P_{D}\left(\delta_{N P}\right)=P_{1}(Y>\eta)=\int_{\eta}^{\infty} y e^{-y} d y=(\eta+1) e^{-\eta}=\alpha(1-\ln \alpha), \quad 0<\alpha<1
$$

#### Solution (c):

Similar as (a), first write the pdf:
$$
p_{0}(y)=\prod_{k=1}^{n} p\left(y_{k}\right)=\prod_{k=1}^{n} e^{-y_{k}}, \quad 0<\min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}
$$
And for $H_1$:
$$
\begin{aligned}
p_{1}(y) &=\int_{-\infty}^{\infty}\left[\prod_{k=1}^{n} p\left(y_{k}-s\right)\right] p(s) d s=\int_{0}^{\min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}}\left[\prod_{k=1}^{n} e^{s-y_{k}}\right] e^{-s} d s \\
=& \frac{p_{0}(y)}{n-1}\left[e^{(n-1) \min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}}-1\right], \quad 0<\min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}
\end{aligned}
$$
Thus, the likelihood ratio can be written as:
$$
L(y)=\frac{1}{n-1}\left[e^{(n-1) \min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}}-1\right], \quad 0<\min \left\{y_{1}, y_{2}, \ldots, y_{n}\right\}
$$

#### Solution (d):

Firstly, write the false alarm probability as:
$$
\begin{aligned}
P_{F}\left(\delta_{N P}\right)=& P_{0}(L(Y)>\eta)=P_{0}\left(\min \left\{Y_{1}, Y_{2}, \ldots, Y_{n}\right\}>\eta^{\prime} \equiv \frac{\log ((n-1) \eta+1)}{n-1}\right) \\
&=P_{0}\left(\bigcap_{k=1}^{n}\left(Y_{k}>\eta^{\prime}\right)\right)=\prod_{k=1}^{n} P_{0}\left(Y_{k}>\eta^{\prime}\right)=\prod_{k=1}^{n} e^{-\eta^{\prime}}=e^{-n \eta^{\prime}}
\end{aligned}
$$
Where the $\eta^{\prime}=-\frac{1}{n} \log \alpha$, and the threshold $\eta$ is:
$$
\eta=\frac{e^{(n-1) \eta^{\prime}}-1}{n-1}=\frac{\alpha^{-(n-1) / n}-1}{n-1}
$$


### 4th problem

![image-20210814203211084](README.assets/image-20210814203211084.png)

The pdf under $H_0,\ H_1$

<img src="README.assets/image-20210816130446578.png" alt="image-20210816130446578" style="zoom:50%;" />

#### Solution (a):

According to $\text { (II.E.31) }$ , the $\alpha$-level $locally\ most\ powerful$ (LMP) test is :
$$
\tilde{\delta}_{l o}(y)= \begin{cases}1 & \text { if }\left.\frac{\partial p_{\theta}(y)}{\partial \theta}\right|_{\theta=0}>\eta p_{0}(y) \\ \gamma, & \text { if }\left.\frac{\partial p_{\theta}(y)}{\partial \theta}\right|_{\theta=0}=\eta p_{0}(y) \\ 0 & \text { if }\left.\frac{\partial p_{\theta}(y)}{\partial \theta}\right|_{\theta=0}<\eta p_{0}(y)\end{cases}
$$
And :
$$
\begin{aligned}
&\left.\frac{\partial p_{\theta}(y)}{\partial \theta}\right|_{\theta=0}=\begin{cases}
\frac{1}{2} e^{-y},\quad& y>0 \\
-\frac{1}{2}e^{-y},\quad& y<0
\end{cases}\\

\Longrightarrow & \frac{\left.\frac{\partial p_{\theta}(y)}{\partial \theta}\right|_{\theta=0}}{p_0(y)}=\begin{cases}1, \quad & y>0\\
0, \quad & y<0
\end{cases}=sgn(y)
\end{aligned}
$$
Thus, 
$$
\tilde{\delta}_{l o}(y)= \begin{cases}1 & \text { if } \operatorname{sgn}(y)>\eta \\ \gamma, & \text { if } \operatorname{sgn}(y)=\eta \\ 0 & \text { if } \operatorname{sgn}(y)<\eta\end{cases}
$$
Since $\alpha = E_0[\tilde{\delta}_{l o}(y)]$ The randomization $\gamma$ is :
$$
\gamma=\frac{\alpha-P_{0}(\operatorname{sgn}(Y)>\eta)}{P_{0}(\operatorname{sgn}(Y)=\eta)}
$$
this implies the range of $\eta$, i.e., $\eta \in \{-1, 1\}$ , notice that $\gamma > 0$, and $P_{0}(\operatorname{sgn}(Y)>\eta)=\begin{cases}0, \ &\eta=1 \\1/2, \ &\eta=-1 \end{cases}$and $P_{0}(\operatorname{sgn}(Y)=\eta)=1/2, \forall \eta \in \{-1, 1 \}$, so the randomization is :
$$
\gamma= \begin{cases}2 \alpha & \text { if } 0<\alpha<1 / 2 \\ 2 \alpha-1 & \text { if } 1 / 2 \leq \alpha<1\end{cases}
$$
The LMP rules is:
$$
\delta_{l o}(y)= \begin{cases}2 \alpha & \text { if } y>0 \\ 0 & \text { if } y \leq 0\end{cases}, \quad \text{for}\ 0<\alpha<1 / 2
$$

$$
\delta_{l o}(y)= \begin{cases}1 & \text { if } y \geq 0 \\ 2 \alpha-1 & \text { if } y<0\end{cases}\quad \text{for}\ 1/2\leq\alpha<1 
$$

The power function is the detection probability :
$$
P_{D}\left(\tilde{\delta}_{l o} ; \theta\right)=P_{\theta}(\operatorname{sgn}(Y)>\eta)+\gamma P_{\theta}(\operatorname{sgn}(Y)=\eta)\\
\begin{gathered}
= \begin{cases}2 \alpha \int_{0}^{\infty} \frac{1}{2} e^{-|y-\theta|} d y & \text { if } 0<\alpha<1 / 2 \\
\int_{0}^{\infty} \frac{1}{2} e^{-|y-\theta|} d y+(2 \alpha-1) \int_{-\infty}^{0} \frac{1}{2} e^{-|y-\theta|} d y & \text { if } 1 / 2 \leq \alpha<1\end{cases} \\
= \begin{cases}\alpha\left(2-e^{-\theta}\right) & \text { if } 0<\alpha<1 / 2 \\
1+(\alpha-1) e^{-\theta} & \text { if } 1 / 2 \leq \alpha<1\end{cases}
\end{gathered}
$$

#### Solution (b):

$\text { the NP critical region is }$
$$
\Gamma_{\theta}=\left\{\frac{p_{\theta}(y)}{p_0(y)}>\eta\right\}=\left\{|y|-|y-\theta|>\eta^{\prime}\right\}
$$
<img src="README.assets/image-20210816160233906.png" alt="image-20210816160233906" style="zoom:50%;" />

According to the figure shown above, the NP critical region is:
$$
\Gamma_{\theta}=\begin{cases}(-\infty, \infty) & \text { if } \eta^{\prime}<-\theta \\ \left(\left(\frac{\eta^{\prime}+\theta}{2}\right), \infty\right) & \text { if }-\theta \leq \eta^{\prime} \leq \theta \\ \phi & \text { if } \eta^{\prime}>\theta\end{cases}
$$
Obviously, the critical region is relevant to the parameter $\theta$, so the UMP test doesn't exist.

The generalized likelihood ratio test uses this statistic:

![image-20210816162007788](README.assets/image-20210816162007788.png)


$$
\begin{aligned}
&\sup _{\theta>0} e^{|y|-|y-\theta|}=\exp \left\{\sup _{\theta>0}(|y|-|y-\theta|)\right\} \\
&= \begin{cases}1 & \text { if } y<0 \\
e^{y} & \text { if } y \geq 0\end{cases}
\end{aligned}
$$


### 5th problem

![image-20210814203233306](README.assets/image-20210814203233306.png)

Similar as $(\text { II.B.6) }$, the overall cost function can be written as:
$$
\begin{gathered}
r(\delta)=\sum_{j=0}^{M-1} \sum_{i=0}^{M-1} \pi_{j} C_{i j} P_{j}\left(\Gamma_{i}\right)=\sum_{i=0}^{M-1}\left[\sum_{j=0}^{M-1} \pi_{j} C_{i j} P_{j}\left(\Gamma_{i}\right)\right] \\
=\sum_{i=0}^{M-1}\left[\sum_{j=0}^{M-1} \pi_{j} C_{i j} \int_{\Gamma_{i}} p_{j}(y) \mu(d y)\right]=\sum_{i=0}^{M-1} \int_{\Gamma_{i}}\left[\sum_{j=0}^{M-1} \pi_{j} C_{i j} p_{j}(y)\right] \mu(d y)
\end{gathered}
$$
in order to minimize the cost $r(\delta)$, each region $\Gamma_i$ should enpower the $\left[\sum_{j=0}^{M-1} \pi_{j} C_{i j} p_{j}(y)\right]$ to be the smallest for $i \in \text{Indexs of all hypothesis}$ then the bayes rule decision regions are defined as:
$$
\Gamma_{i}=\left\{y \in \Gamma \mid \sum_{j=0}^{M-1} \pi_{j} C_{i j} p_{j}(y)=\min _{0 \leq k \leq M-1} \sum_{j=0}^{M-1} \pi_{j} C_{k j} p_{j}(y)\right\}
$$


### 6th problem

![image-20210814203251623](README.assets/image-20210814203251623.png)

#### solution (a):

the pdf for $H_0, \ H_1$ are:
$$
p_1(y)  =\prod_{k=1}^{n} \frac{1}{\sqrt{2 \pi} \sigma_{0}} e^{-\left(y_{k}-\mu_{0}\right)^{2} / 2 \sigma_{0}^{2}}
$$
and
$$
p_0(y)=\prod_{k=1}^{n} \frac{1}{\sqrt{2 \pi} \sigma_{1}} e^{-\left(y_{k}-\mu_{1}\right)^{2} / 2 \sigma_{1}^{2}}
$$
So the likehood ratio is:
$$
\begin{gathered}
L(y)=\frac{\prod_{k=1}^{n} \frac{1}{\sqrt{2 \pi} \sigma_{1}} e^{-\left(y_{k}-\mu_{1}\right)^{2} / 2 \sigma_{1}^{2}}}{\prod_{k=1}^{n} \frac{1}{\sqrt{2 \pi} \sigma_{0}} e^{-\left(y_{k}-\mu_{0}\right)^{2} / 2 \sigma_{0}^{2}}} \\
=\left(\frac{\sigma_{0}}{\sigma_{1}}\right)^{n} e^{\frac{n}{2}\left(\frac{\mu_{0}^{2}}{\sigma_{0}^{2}}-\frac{\mu_{1}^{2}}{\sigma_{1}^{2}}\right)} e^{\left(\frac{1}{2 \sigma_{0}^{2}}-\frac{1}{2 \sigma_{1}^{2}}\right) \sum_{k=1}^{n} y_{k}^{2}} e^{\left(\frac{\mu_{1}}{\sigma_{1}^{2}}-\frac{\mu_{0}}{\sigma_{0}^{2}}\right) \sum_{k=1}^{n} y_{k}}
\end{gathered}
$$

#### Solution (b):

1) if $\left.(\mu_0=\mu_{1}, \sigma_{1}^{2}>\sigma_{0}^{2}\right)$

in this case, the likehood ratio become:
$$
L(y)=\left(\frac{\sigma_0}{\sigma_1}\right)^ne^{\left( \frac{1}{2\sigma_0^2}- \frac{1}{2\sigma_1^2} \right)\cdot \sum_{k=1}^n(y_k-\mu)^2}
$$
So the Neyman-Pearson test operates by comparing $\sum_{k=1}^n(y_k-\mu)^2$  to a threshold

2) if $\left(\sigma_{0}^{2}=\sigma_{1}^{2}, \mu_{1}>\mu_{0}\right)$

in this case, the likehood ratio become:
$$
L(y) = exp\left(2(\mu_1-\mu_0 )\cdot\sum_{k= 1}^{n}y_k+n\cdot(\mu_0-\mu_1) \right)
$$
So the Neyman-Pearson test operates by comparing $\sum_{k=1}^ny_k$  to a threshold

#### Solution (c):

in this case, the likehood ratio become:
$$
\begin{aligned}
L(y)&=\left(\frac{\sigma_0}{\sigma_1}\right)^ne^{\left( \frac{1}{2\sigma_0^2}- \frac{1}{2\sigma_1^2} \right)\cdot \sum_{k=1}^n(y_k-\mu)^2}\\
&=\frac{\sigma_0}{\sigma_1}\cdot e^{\left( \frac{1}{2\sigma_0^2}- \frac{1}{2\sigma_1^2} \right)\cdot (y_1-\mu)^2}
\end{aligned}
$$
The form of the NP test is:
$$
\delta_{N P}(y)= \begin{cases}1 & \text { if }\left(y_{1}-\mu\right)^{2} \geq \eta^{\prime} \\ 0 & \text { if }\left(y_{1}-\mu\right)^{2}<\eta^{\prime}\end{cases}
$$




write the false-alarm probability as:
$$
\begin{aligned}
P_0(p_1(Y)>\eta \cdot p_0(Y))&=P_0(L(Y)>\eta)\\
&=P_0((y_1-\mu)^2>\eta^{'})\\
&=2\left[1-\Phi\left(\frac{\sqrt{\eta^{\prime}}}{\sigma_{0}}\right)\right]
\end{aligned}
$$
since $P_0(p_1(Y)>\eta\cdotp_0(Y))=P_F(\delta_{NP})=\alpha$ , so for the $\alpha$ the threshold $\eta$ is set as :
$$
\eta^{\prime}=\left[\sigma_{0} \Phi^{-1}\left(1-\frac{\alpha}{2}\right)\right]^{2}
$$
and the detection probability is :
$$
\begin{aligned}
P_{D}\left(\delta_{N P}\right) 
&=P_1(\Gamma_1)=P_1\left(Y_1-\mu<-\sqrt{\eta^{\prime}}\ \cup Y_1-\mu>\sqrt{\eta^{\prime}}\right)\\

&=1-P_{1}\left(-\sqrt{\eta^{\prime}} \leq Y_{1}-\mu \leq \sqrt{\eta^{\prime}}\right)=2\left[1-\Phi\left(\frac{\sqrt{\eta^{\prime}}}{\sigma_{1}}\right)\right] \\
&=2\left[1-\Phi\left(\frac{\sigma_{0}}{\sigma_{1}} \Phi^{-1}\left(1-\frac{\alpha}{2}\right)\right)\right], \quad 0<\alpha<1
\end{aligned}
$$
