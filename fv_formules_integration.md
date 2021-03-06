+++
title = "Formules d'intégration"

date = 2018-09-09T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = true

# Add menu entry to sidebar.
[menu.fem]
  parent = "menu_fv"
  name = "Formules d'intégration"
  weight = 20


+++

$\newcommand{\Cb}{\mathbb{C}}$
$\newcommand{\Rb}{\mathbb{R}}$
$\newcommand{\PS}[2]{\left(#1,#2\right)}$
$\newcommand{\norm}[1]{\left\\|#1\right\\|}$
$\newcommand{\abs}[1]{\left|#1\right|}$
$\newcommand{\xx}{\mathbf{x}}$
$\newcommand{\yy}{\mathbf{y}}$
$\newcommand{\zz}{\mathbf{z}}$
$\newcommand{\nn}{\mathbf{n}}$
$\newcommand{\Ccal}{\mathcal{C}}$
$\newcommand{\Cscr}{\mathscr{C}}$
$\newcommand{\omegai}{\omega\_i}$
$\newcommand{\dsp}{\displaystyle}$
$\newcommand{\diff}{{\rm d}}$
$\newcommand{\divv}{{\rm div}}$
$\newcommand{\rot}{\mathbf{rot}}$
$\newcommand{\phii}{\phi\_i}$
$\newcommand{\yN}{y\_N}$

## Régularité du domaine

Dans ce cours, les domaines $\Omega$ seront des ouverts *réguliers* de $\Rb^d$, au moins de classe $\Cscr^1$. La quantité $d= 2,3$ est la dimension du problème considéré. Nous pouvons ainsi définir le vecteur unitaire normale $\nn$ sortant à $\Omega$.

{{% thm definition %}}
Un ouvert $\Omega$ de $\Rb^d$ est régulier de classe $\Cscr^k$ ($k\geq 1$) s'il existe un nombre fini d'ouverts $(\omegai)\_{0\leq i\leq I}$ tels que
$$
\overline{\omega\_0}\subset\Omega, \qquad \overline{\Omega}\subset \bigcup\_{i=1}^I\omega\_i, \qquad \partial\Omega \subset \bigcup\_{i=1}^I \omega\_i,
$$
et que, pour chaque $i\in\{1,\ldots,I\}$, il existe une application bijective $\phii$ de classe $\Ccal^k$, de $\omega\_i$ dans l'ensemble
$$
Q = \left\\{ y = (y', \yN)\in\Rb^{N-1}\times\Rb, \abs{y'}< 1, \abs{\yN}<1 \right\},
$$
dont l'inverse est aussi de classe $\Ccal^k$, et telle que
$$
\begin{array}{l}
\phii(\omegai\cap\Omega) = Q \cap \{y = (y', \yN)\in\Rb^{N-1}\times\Rb,  \yN > 0 \\} = Q^+, \\\\\\
\phii(\omegai\cap\partial\Omega) = Q \cap \\{y = (y', \yN)\in\Rb^{N-1}\times\Rb,  \yN = 0\\}.
\end{array}
$$
{{% /thm %}}

Remarquons que nombreux résultats d'intégration que nous énoncerons restent vrais pour un domaine à bord polygonal, et retenons surtout que les domaines considérés ne comportent ni "fissure" ni point de rebroussement, et leur frontière est "régulière", comme illustré sur la figure ci-dessous.

{{< figure src="/img/course/fem/regulier.svg" title="Ouvert régulier (à gauche), avec point de rebroussement (milieu) et \"fissure\" (à droite). Les deux derniers ouverts ne sont pas réguliers" numbered="true" >}}


## Formules de Green

Nous admettrons le théorème suivant, résultat central dans l'analyse des EDP.

{{% thm theorem "de Green" %}}
Soit $\Omega$ un ouvert borné, régulier de classe $\Cscr^1$ de $\Rb^d$. Si $w$ est une fonction de $\Cscr^1(\overline{\Omega})$ alors elle vérifie la formule de Green
$$
\int\_{\Omega}\frac{\partial w}{\partial x\_i}(x)\diff x = \int\_{\partial \Omega}w(x)n\_i(x)\diff s,
$$
où $n\_i$ est la $n^{ème}$ composante de la normale extérieure $\nn$ à $\Omega$.
{{% /thm %}}

{{< figure src="/img/course/fem/normal.svg" title="Normale unitaire $\nn$ extérieure sortante à $\Omega$" numbered="true" >}}

De ce Théorème fondamental découlent des Corollaires qui nous seront pratiques. Par exemple, si l'on prend $w=uv$ dans la formule précédente, il vient :

{{% thm corollary "Formule d'intégration par parties" %}}
Soit $\Omega$ un ouvert borné, régulier de classe $\Cscr^1$. Soit $u$ et $v$ deux fonctions de $\Cscr^1(\overline{\Omega})$, alors elles vérifient la formule d'intégration par parties
$$
\int\_{\Omega}\frac{\partial u}{\partial x\_i}(x)v(x)\diff x =
-\int\_{\Omega}v(x)\frac{\partial v}{\partial x\_i}(x)\diff x
+ \int\_{\partial\Omega}u(x)v(x)n\_i(x)\diff s.
$$
{{% /thm %}}

En supposant $u\in\Cscr^2(\overline{\Omega})$, soit à peine plus régulier, nous pouvons appliquer le corollaire précédent pour obtenir :

{{% thm corollary "Formule de Green" %}}
Soit $\Omega$ un ouvert borné, régulier de classe $\Cscr^1$. Deux fonctions $u\in\Cscr^2(\overline{\Omega})$ et $v\in\Cscr^1(\overline{\Omega})$ vérifient la Formule de Green :
$$
\int\_{\Omega}\Delta u(x)v(x)\diff x =
-\int\_{\Omega}\nabla u(x)\cdot \nabla v(x) \diff x
+ \int\_{\partial\Omega}\frac{\partial u}{\partial \nn}(x)v(x)\diff s,
$$
où $\nabla u = \left(\frac{\partial u}{\partial x\_i}\right)\_{1\leq i \leq d}$ est le vecteur gradient de $u$, et $\frac{\partial u}{\partial \nn} = \nabla u \cdot \nn$.
{{% /thm %}}


## Autres formules d'intégration

Nous considérons ici $\Omega$ un ouvert borné et régulier de classe $\Cscr^1$. On supposera $u,v, \phi, \psi$ et $\sigma$
sont suffisamment dérivables à chaque fois.  Nous rappelons les opérateurs suivants :

- La divergence d'un vecteur $\sigma$
$$
\divv(\sigma) = \sum\_{i=1}^d \frac{\partial \sigma}{\partial x\_i}.
$$
- Le rotationnel d'un vecteur $\phi$
$$
\rot \phi = \left(\frac{\partial \phi\_3}{\partial x\_2} - \frac{\partial \phi\_2}{\partial x\_3},
\frac{\partial \phi\_1}{\partial x\_3} - \frac{\partial \phi\_3}{\partial x\_1},
\frac{\partial \phi\_2}{\partial x\_1} - \frac{\partial \phi\_1}{\partial x\_2}
\right)
$$
- Le produit vectoriel $\times$ entre deux vecteurs $\phi$ et $\psi$
$$
\phi\times \psi = 
\\left(
  \begin{array}{l}
  \phi\_2\psi\_3 - \phi\_3\psi\_2\\\\\\
  \phi\_3\psi\_1 - \phi\_1\psi\_3\\\\\\
  \phi\_1\psi\_2 - \phi\_2\psi\_1\\\\\\
  \end{array}
\right)
$$


{{% alert exercise %}}
À l'aide de la formule de Green, montrez les formules suivantes (vous pouvez développer les expressions...):

1. **La formule du Laplacien :**
$$
\int\_{\Omega}\Delta u(x)v(x)\diff x = -
\int\_{\Omega}\nabla u(x)\cdot \nabla v(x) \diff x +
\int\_{\partial\Omega}\frac{\partial u}{\partial \nn}(x)v(x)\diff s,
$$
où $\nabla u = \left(\frac{\partial u}{\partial x\_i}\right)\_{1\leq i \leq d}$ est le vecteur gradient de $u$, et $\frac{\partial u}{\partial \nn} = \nabla u \cdot \nn$.
2. **La formule de Stokes :**
$$
\int\_{\Omega}\divv \sigma(x) \phi(x)\diff x = -
\int\_{\Omega} \sigma(x)\cdot\nabla \phi(x)\diff x +
\int\_{\partial\Omega}\sigma(x)\cdot\nn(x)\phi(x)\diff s.
$$
3. **La formule du rotationnel :**
$$
\int\_{\Omega}\rot \phi \cdot \psi\diff x -
\int\_{\Omega} \phi\cdot\rot \psi \diff x =-
\int\_{\partial\Omega}(\phi\times\nn)\cdot \psi \diff s,
$$

{{% /alert %}}

<!-- 
\begin{correction}
  \begin{enumerate}
  \item Nous pouvons calculer direction par direction (l'inversion somme-intégrale est rendue possible puisque $\Omega$ est borné et la somme finie) :
    $$
      \int\_{\Omega}\Delta u(x)v(x)\diff x =
      \int\_{\Omega}\sum_{j=1}^3\frac{\partial^2 u}{\partial x_j^2}(x) v(x) \diff x =
      \sum_{j=1}^3\int\_{\Omega}\frac{\partial^2 u}{\partial x_j^2}(x) v(x) \diff x.
    $$
Nous appliquons ensuite la formule de Green et re-regroupons les sommes :
$$
  \begin{array}{r c l}
\dsp      \sum_{j=1}^3\int\_{\Omega}\frac{\partial^2 u}{\partial x_j^2}(x) v(x) \diff x
      &=&
    \dsp  \sum_{j=1}^3\left[-\int\_{\Omega}\frac{\partial u}{\partial x_j}(x)\frac{\partial v}{\partial x_j}(x) \diff x
      +\int\_{\partial\Omega}\frac{\partial u}{\partial x_j}(x)v(x)n_j(x) \diff x\right]\\
\dsp     & =&
\dsp      -\int\_{\Omega}\sum_{j=1}^3\frac{\partial u}{\partial x_j}(x)\frac{\partial v}{\partial x_j}(x) \diff x
              +\int\_{\partial\Omega}\sum_{j=1}^3\left[\frac{\partial u}{\partial x_j}(x)n_j(x)\right]v(x) \diff x\\
      & =&\dsp -\int\_{\Omega}\nabla u(x)\cdot\nabla v(x) \diff x
           +\int\_{\partial\Omega}(\nabla u(x)\cdot \nn(x)) v(x)n_j(x) \diff x.
  \end{array}
    $$
    Comme $\nabla u(x)\cdot\nn(x) = \dn u(x)$, le résultat est démontré.
  \item Nous appliquons la même idée :
    $$
      \begin{array}{>{\dsp}r c >{\dsp}l}
        \int\_{\Omega}\divv \sigma(x) \phi(x)\diff x
        &=& \int\_{\Omega}\sum_{j=1}^3\frac{\partial  \sigma_j}{\partial x_j}(x) \phi(x)\diff x \\
        &=&  \sum_{j=1}^3 \int\_{\Omega}\frac{\partial  \sigma_j}{\partial x_j}(x) \phi(x)\diff x.
      \end{array}
    $$
    À l'aide de la formule de Green, nous obtenons
    $$
      \begin{array}{>{\dsp}r c >{\dsp}l}
        \sum_{j=1}^3 \int\_{\Omega}\frac{\partial  \sigma_j}{\partial x_j}(x) \phi(x)\diff x
        & = & \sum_{j=1}^3 \left[-\int\_{\Omega}\sigma_j(x) \frac{\partial\phi}{\partial x_j}(x)\diff x
              +\int\_{\partial\Omega}\sigma_j(x) \phi(x) n_j(x)\diff s\right]\\
        & = &  -\int\_{\Omega} \sum_{j=1}^3\left[\sigma_j(x)\frac{\partial\phi}{\partial x_j}(x)\right]\diff x   +\int\_{\partial\Omega} \sum_{j=1}^3\left[\sigma_j(x) n_j(x)\right]\phi(x) \diff s\\
        & = &  -\int\_{\Omega} \sigma(x)\cdot \nabla\phi(x)\diff x
              +\int\_{\partial\Omega} (\sigma(x) \cdot\nn(x))\phi(x) \diff s.\\
      \end{array}
    $$
  \item Pour simplifier, nous notons $\partial_j = \frac{\partial}{\partial x_j}$ :
    $$
      \begin{array}{>{\dsp}r c >{\dsp}l}
        \int\_{\Omega}\rot \phi \cdot \psi\diff x
        & = & \int\_{\Omega}\left[\partial_2\phi\_3 - \partial_3\phi\_2\right]\psi_1
              +\left[\partial_3\phi\_1 - \partial_1\phi\_3\right]\psi_2
              +\left[\partial_1\phi\_2 - \partial_2\phi\_1\right]\psi_3\diff x\$$0.2cm]
        & = & - \int\_{\Omega} \phi\_3\partial_2\psi_1 - \phi\_2\partial_3\psi_1
              +\phi\_1\partial_3\psi_2 - \phi\_3\partial_1\psi_2
              +\phi\_2\partial_1\psi_3 - \phi\_1\partial_2\psi_3\diff x\$$0.2cm]
        &   & \quad+ \int\_{\partial\Omega}\left[\phi\_3n_2 - \phi\_2n_3\right]\psi_1
              +\left[\phi\_1n_3 - \phi\_3n_1\right]\psi_2
              +\left[\phi\_2n_1 - \phi\_1n_2\right]\psi_3
              \diff s\$$0.2cm]
        & = & - \int\_{\Omega}
              \left[\partial_3\psi_2-\partial_2\psi_3\right]\phi\_1+
              \left[\partial_1\psi_3-\partial_3\psi_1\right]\phi\_2+
              \left[\partial_2\psi_1-\partial_1\psi_2\right]\phi\_3\$$0.2cm]
        &   & \quad+ \int\_{\partial\Omega}(\phi\times\nn)\cdot\psi
              \diff s\$$0.2cm]
        & = & \int\_{\Omega} \phi\cdot\rot \psi \diff x + \int\_{\partial\Omega}(\phi\times\nn)\cdot\psi
              \diff s\\
      \end{array}
    $$
    
  \end{enumerate}
\end{correction} -->