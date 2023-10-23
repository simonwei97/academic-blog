---
title: Latex 公式
subtitle: 简要介绍 Latex 公式使用。

# Summary for listings and search engines
summary: 简要介绍 Latex 公式使用

# Link this post with a project
projects: []

# Date published
date: "2022-12-13T00:00:00Z"

# Date updated
lastmod: "2022-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Latex

categories:
  - 教程
# Book page type (do not modify).
# type: book
---

- 行内公式：两个美元符号扩起来 `$ 公式 $`，或者 `\( 公式 \)`
- 行间公式：
  - 不带编号的写法：两对美元符号扩起来 `$$ 公式 $$`，或者 `\[ 公式 \]`
  - 带自动编号的写法：`\begin{equation} 公式 \end{equation}`。

## 希腊字母

### 小写

|    输入     |     显示      |   输入    |    显示     |   输入    |    显示     |   输入   |    显示    |
| :---------: | :-----------: | :-------: | :---------: | :-------: | :---------: | :------: | :--------: |
|   \alpha    |   $\alpha$    |   \beta   |   $\beta$   |  \gamma   |  $\gamma$   |  \delta  |  $\delta$  |
|  \epsilon   |  $\epsilon$   |   \zeta   |   $\zeta$   |   \eta    |   $\eta$    |  \theta  |  $\theta$  |
|    \iota    |    $\iota$    |  \kappa   |  $\kappa$   |  \lambda  |  $\lambda$  |   \mu    |   $\mu$    |
|     \nu     |     $\nu$     |    \xi    |    $\xi$    |    \pi    |    $\pi$    |   \rho   |   $\rho$   |
|   \sigma    |   $\sigma$    |   \tau    |   $\tau$    | \upsilon  | $\upsilon$  |   \phi   |   $\phi$   |
|    \chi     |    $\chi$     |   \psi    |   $\psi$    |  \omega   |  $\omega$   |          |            |
| \varepsilon | $\varepsilon$ | \vartheta | $\vartheta$ | \varkappa | $\varkappa$ |  \varpi  |  $\varpi$  |
|   \varrho   |   $\varrho$   | \varsigma | $\varsigma$ |  \varphi  |  $\varphi$  | \digamma | $\digamma$ |

### 大写

|   输入    |    显示     |   输入    |    显示     |   输入    |    显示     |    输入     |     显示      |
| :-------: | :---------: | :-------: | :---------: | :-------: | :---------: | :---------: | :-----------: |
|  \Gamma   |  $\Gamma$   |  \Delta   |  $\Delta$   |  \Theta   |  $\Theta$   |   \Lambda   |   $\Lambda$   |
|    \Xi    |    $\Xi$    |    \Pi    |    $\Pi$    |  \Sigma   |  $\Sigma$   |  \Upsilon   |  $\Upsilon$   |
|   \Phi    |   $\Phi$    |   \Psi    |   $\Psi$    |  \Omega   |  $\Omega$   |             |               |
| \varGamma | $\varGamma$ | \varDelta | $\varDelta$ | \varTheta | $\varTheta$ | \varLambda  | $\varLambda$  |
|  \varXi   |  $\varXi$   |  \varPi   |  $\varPi$   | \varSigma | $\varSigma$ | \varUpsilon | $\varUpsilon$ |
|  \varPhi  |  $\varPhi$  |  \varPsi  |  $\varPsi$  | \varOmega | $\varOmega$ |             |               |

## 概率论相关

| 小写形式 | 大写形式 |  变量形式   |                    显示                     |
| :------: | :------: | :---------: | :-----------------------------------------: |
| \epsilon |    E     | \varepsilon | $\epsilon$ $\mid$ $E$ $\mid$ $\varepsilon$  |
|  \theta  |  \Theta  |  \vartheta  | $\theta$ $\mid$ $\Theta$ $\mid$ $\vartheta$ |
|   \rho   |    P     |   \varrho   |     $\rho$ $\mid$ $P$ $\mid$ $\varrho$      |
|  \sigma  |  \Sigma  |  \varsigma  | $\sigma$ $\mid$ $\Sigma$ $\mid$ $\varsigma$ |
|   \phi   |   \Phi   |   \varphi   |    $\phi$ $\mid$ $\Phi$ $\mid$ $\varphi$    |

## 关系运算符

|   输入   |    显示    |    输入    |      显示      |   输入    |    显示     |    输入    |     显示     |
| :------: | :--------: | :--------: | :------------: | :-------: | :---------: | :--------: | :----------: |
|   \pm    |   $\pm$    |   \times   |    $\times$    |   \div    |   $\div$    |    \mid    |    $\mid$    |
|  \nmid   |  $\nmid$   |   \cdot    |    $\cdot$     |   \circ   |   $\circ$   |    \ast    |    $\ast$    |
| \bigodot | $\bigodot$ | \bigotimes | $\bigotimes$ o | \bigoplus | $\bigoplus$ |    \leq    |    $\leq$    |
|   \geq   |   $\geq$   |    \neq    |     $\neq$     |  \approx  |  $\approx$  |   \equiv   |   $\equiv$   |
|   \sum   |   $\sum$   |   \prod    |    $\prod$     |  \coprod  |  $\coprod$  | \backslash | $\backslash$ |

## 集合运算符

|   输入    |    显示     |   输入    |    显示     |   输入    |    显示     |
| :-------: | :---------: | :-------: | :---------: | :-------: | :---------: |
| \emptyset | $\emptyset$ |    \in    |    $\in$    |  \notin   |  $\notin$   |
|  \subset  |  $\subset$  |  \supset  |  $\supset$  | \subseteq | $\subseteq$ |
| \supseteq | $\supseteq$ |  \bigcap  |  $\bigcap$  |  \bigcup  |  $\bigcup$  |
|  \bigvee  |  $\bigvee$  | \bigwedge | $\bigwedge$ | \biguplus | $\biguplus$ |

## 对数运算符

| 输入 |  显示  | 输入 | 显示  | 输入 | 显示  |
| :--: | :----: | :--: | :---: | :--: | :---: |
| \log | $\log$ | \lg  | $\lg$ | \ln  | $\ln$ |

## 三角运算符

|   输入   |    显示    | 输入 |  显示  |   输入   |    显示    |
| :------: | :--------: | :--: | :----: | :------: | :--------: |
| 30^\circ | $30^\circ$ | \bot | $\bot$ | \angle A | $\angle A$ |
|   \sin   |   $\sin$   | \cos | $\cos$ |   \tan   |   $\tan$   |
|   \csc   |   $\csc$   | \sec | $\sec$ |   \cot   |   $\cot$   |

## 微积分运算符

|  输入   |   显示    |  输入  |   显示   |  输入  |   显示   |
| :-----: | :-------: | :----: | :------: | :----: | :------: |
|  \int   |  $\int$   | \iint  | $\iint$  | \iiint | $\iiint$ |
| \iiiint | $\iiiint$ | \oint  | $\oint$  | \prime | $\prime$ |
|  \lim   |  $\lim$   | \infty | $\infty$ | \nabla | $\nabla$ |

## 箭头符号

|        输入         |         显示          |        输入         |          显示          |
| :-----------------: | :-------------------: | :-----------------: | :--------------------: |
|      \uparrow       |      $\uparrow$       |      \Uparrow       |      $\Uparrow $       |
|     \downarrow      |     $\downarrow$      |     \Downarrow      |     $\Downarrow $      |
|     \leftarrow      |     $\leftarrow$      |     \Leftarrow      |     $\Leftarrow $      |
|     \rightarrow     |     $\rightarrow$     |     \Rightarrow     |     $\Rightarrow $     |
|   \leftrightarrow   |   $\leftrightarrow$   |   \Leftrightarrow   |   $\Leftrightarrow $   |
|   \longleftarrow    |   $\longleftarrow$    |   \Longleftarrow    |   $\Longleftarrow $    |
|   \longrightarrow   |   $\longrightarrow$   |   \Longrightarrow   |   $\Longrightarrow $   |
| \longleftrightarrow | $\longleftrightarrow$ | \Longleftrightarrow | $\Longleftrightarrow $ |

## 省略号

|  输入  |   显示   |  输入  |   显示   |  输入  |   显示   |
| :----: | :------: | :----: | :------: | :----: | :------: |
| \dots  | $\dots$  | \ldots | $\ldots$ | \cdots | $\cdots$ |
| \vdots | $\vdots$ | \ddots | $\ddots$ |        |          |
