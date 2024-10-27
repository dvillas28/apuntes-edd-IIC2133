#clase00
## Definición

### Notación $\mathcal{O}$
$$\mathcal{O}(g) = \{g:\mathbb{N} \rightarrow \mathbb{R}^+ | (\exists c \in \mathbb{R}^+)(\exists n_o \in \mathbb{N})(\forall n \geq n_o)(f(n) \leq cg(n)) \}$$

![[Pasted image 20240805144315.png]]

Si $f \in \mathcal{O}(g)$ entonces f **crece más lento o igual que** $g$

### Notación $\Omega$
$$\Omega(g) = \{g:\mathbb{N} \rightarrow \mathbb{R}^+ | (\exists c \in \mathbb{R}^+)(\exists n_o \in \mathbb{N})(\forall n \geq n_o)(f(n) \geq cg(n)) \}$$

#### Otra definición
Se define el conjunto $\Omega(g)$ tal que
$$f \in \Omega(g) \leftrightarrow g \in \mathcal{O}(f)$$

![[Pasted image 20240805144842.png]]

Si $f \in \Omega(g)$ entonces f **crece más rápido o igual que** $g$

### Notación $\Theta$
Para $g: \mathbb{N} \rightarrow \mathbb{R}^+$ se define el conjunto de funciones $\Theta(g)$ tal que
$$f \in \Theta(g) \leftrightarrow f \in \mathcal{O}(g) \land f \in \Omega(g)$$

![[Pasted image 20240805145127.png]]

Si $f \in \Theta(g)$ entonces f **crece igual que** $g$