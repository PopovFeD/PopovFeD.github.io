Это тестовый проект, идею которого подкинул мне мой отец. Если всё получится, результат будет замечательным.

$$
\begin{array}{rll}
E \psi &= H\psi & \text{Expanding the Hamiltonian Operator} \\
&= -\frac{\hbar^2}{2m}\frac{\partial^2}{\partial x^2} \psi + \frac{1}{2}m\omega x^2 \psi & \text{Using the ansatz $\psi(x) = e^{-kx^2}f(x)$, hoping to cancel the $x^2$ term} \\
&= -\frac{\hbar^2}{2m} [4k^2x^2f(x)+2(-2kx)f'(x) + f''(x)]e^{-kx^2} + \frac{1}{2}m\omega x^2 f(x)e^{-kx^2} &\text{Removing the $e^{-kx^2}$ term from both sides} \\
& \Downarrow \\
Ef(x) &= -\frac{\hbar^2}{2m} [4k^2x^2f(x)-4kxf'(x) + f''(x)] + \frac{1}{2}m\omega x^2 f(x) & \text{Choosing $k=\frac{im}{2}\sqrt{\frac{\omega}{\hbar}}$ to cancel the $x^2$ term, via $-\frac{\hbar^2}{2m}4k^2=\frac{1}{2}m \omega$} \\
&= -\frac{\hbar^2}{2m} [-4kxf'(x) + f''(x)] \\
\end{array}
$$

![[tttt.png]]
