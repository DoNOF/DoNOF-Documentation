# Occupation Mapping



$\eta_g = \frac{1}{2}( 1 + \cos^2 \gamma_g)$

$\eta_{p_1} = h_g \sin^2 \gamma_{p_1}$

$\eta_{p_2} = h_g \cos^2 \gamma_{p_1} \sin^2 \gamma_{p_2}$

$\eta_{p_3} = h_g \cos^2 \gamma_{p_1} \cos^2 \gamma_{p_2} \sin^2 \gamma_{p_3}$

$\eta_{p_4} = h_g \cos^2 \gamma_{p_1} \cos^2 \gamma_{p_2} \cos^2 \gamma_{p_3}$


---

*Remember: $\cos^2 \gamma + \sin^2 \gamma = 1$*



---

${\color{orange} {h_{g}}} = {\color{orange}{ 1 - \eta_g}}$

${\color{blue}{h_{p_1}}} = h_g \cos^2 \gamma_{p_1} = h_g( 1 - \sin^2 \gamma_{p_1}) = h_g - h_g \sin^2 \gamma_{p_1} = {\color{blue}{1 - \eta_g - \eta_{p_1}}}$

${\color{purple} {h_{p_2}}}= h_{p_1} \cos^2 \gamma_{p_2} = h_{p_1}( 1 - \sin^2 \gamma_{p_2} ) = h_{p_1} - h_{p_1} \sin^2 \gamma_{p_2} = {\color{purple}{ (1 - \eta_g - \eta_{p_1}) - \eta_{p_2}}}$

${\color{brown}{ h_{p_3}}} = h_{p_2} \cos^2 \gamma_{p_3} = h_{p_2}( 1 - \sin^2 \gamma_{p_3} ) = h_{p_2} - h_{p_2} \sin^2 \gamma_{p_3} = {\color{brown}{ 1 - \eta_g - \eta_{p_1} - \eta_{p_2} - \eta_{p_3}}}$


---

*Hence*

${\eta_g = \frac{1}{2} ( 1 + \cos^2 \gamma_{g} )}$

${\eta_{p_1} = {\color{orange}h_g} \sin^2 \gamma_{p_1} = ({\color{orange}{ 1 - \eta_g}}) \sin^2 \gamma_{p_1}}$

${\eta_{p_2} = {\color{blue}{h_g \cos^2 \gamma_{p_1} }}\sin^2 \gamma_{p_2} = {\color{blue}{h_{p_1}}} \sin^2 \gamma_{p_2} = ({\color{blue}{1 - \eta_g - \eta_{p_1}}}) \sin^2 \gamma_{p_2}}$

${\eta_{p_3} = {\color{purple}{h_g \cos^2 \gamma_{p_1} \cos^2 \gamma_{p_2}}} \sin^2 \gamma_{p_3} = {\color{purple}{h_{p_2}}} \sin^2 \gamma_{p_3} = ({\color{purple}{1 - \eta_g - \eta_{p_1} - \eta_{p_2}}}) \sin^2 \gamma_{p_3}}$

${\eta_{p_4} = {\color{brown}{h_g \cos^2 \gamma_{p_1} \cos^2 \gamma_{p_2} \cos^2 \gamma_{p_3} }}={{\color{brown} {h_{p_3}}}} = {\color{brown}{1 - \eta_g - \eta_{p_1} - \eta_{p_2} - \eta_{p_3}}}}$

The possible derivatives are:

| 1 | 2 | 3 | 4 |
|---|---|---|---|
|$\frac{\partial \eta_g}{\partial \gamma_g} = -\frac{1}{2} \sin ( 2 \gamma_g)$ | | | |
|$\frac{\partial \eta_{p_1}}{\partial \gamma_g} = - \frac{\partial \eta_g}{\partial \gamma_g} \sin^2(\gamma_{p_1})$ | $\frac{\partial \eta_{p_1}}{\partial \gamma_{p_1}} = \eta_g \sin ( 2 \gamma_{p_1})$ | | |
|$\frac{\partial \eta_{p_2}}{\partial \gamma_g} =  (- \frac{\partial \eta_g}{\partial \gamma_g} -\frac{\partial\eta_{p_1}}{\partial\gamma_g}) \sin^2(\gamma_{p_2})$ | $\frac{\partial \eta_{p_2}}{\partial \gamma_{p_1}} = - \frac{\partial \eta_{p_1}}{\partial \gamma_{p_1}} \sin^2(\gamma_{p_2})$ | $\frac{\partial \eta_{p_2}}{\partial \gamma_{p_2}} = (1-\eta_g-\eta_{p_1})\sin^2(2\gamma_{p_2})$ | |
|$\frac{\partial \eta_{p_3}}{\partial \gamma_g} = (- \frac{\partial \eta_g}{\partial \gamma_g}-\frac{\partial\eta_{p_1}}{\partial\gamma_g}-\frac{\partial\eta_{p_2}}{\partial\gamma_g}) \sin^2(\gamma_{p_3})$ | $\frac{\partial \eta_{p_3}}{\partial \gamma_{p_1}} =  (- \frac{\partial \eta_{p_1}}{\partial \gamma_{p_1}} -\frac{\partial\eta_{p_2}}{\partial\gamma_{p_1}} )\sin^2(\gamma_{p_3})$ | $\frac{\partial \eta_{p_3}}{\partial \gamma_{p_2}} = -\frac{\partial\eta_{p_2}}{\partial \gamma_{p_2}} \sin^2 (\gamma_{p_3})$ | $\frac{\partial \eta_{p_3}}{\partial \gamma_{p_3}} = (1-\eta_g-\eta_{p_1}-\eta_{p_2})\sin(2\gamma_{p_3})$ |
|$\frac{\partial \eta_{p_4}}{\partial \gamma_g} = (- \frac{\partial \eta_g}{\partial \gamma_g}-\frac{\partial\eta_{p_1}}{\partial\gamma_g}-\frac{\partial\eta_{p_2}}{\partial\gamma_g}-\frac{\partial\eta_{p_3}}{\partial\gamma_g})$ | $\frac{\partial \eta_{p_4}}{\partial \gamma_{p_1}} = - \frac{\partial \eta_{p_1}}{\partial \gamma_{p_1}}-\frac{\partial\eta_{p_2}}{\partial\gamma_{p_1}}-\frac{\partial\eta_{p_3}}{\partial\gamma_{p_1}}$ | $\frac{\partial \eta_{p_4}}{\partial \gamma_{p_2}} = -\frac{\partial\eta_{p_2}}{\partial \gamma_{p_2}} -\frac{\partial\eta_{p_3}}{\partial\gamma_{p_2}}$ | $\frac{\partial \eta_{p_4}}{\partial \gamma_{p_3}} = -\frac{\partial\eta_{p_3}}{\partial \gamma_{p_3}}$ |


 Generalizing:


\begin{array}{llll}
\frac{\partial \eta_{{\color{green}g}}}{\partial \gamma_{\color{green}g}} = -\frac{1}{2} \sin(2\gamma_g) & & & \\
\\
\frac{\partial \eta_{p_{\color{brown}i}}}{\partial \gamma_{\color{brown}g}} = -(\frac{\partial\eta_g}{\partial\gamma_g}+\sum_{k=1}^{i-1}\frac{\partial\eta_{p_k}}{\partial\gamma_g})\sin^2(\gamma_{p_i}) &
\frac{\partial \eta_{p_{\color{brown}i}}}{\partial \gamma_{\color{brown}{j<i}}} = -(\sum_{k=j}^{i-1}\frac{\partial\eta_{p_k}}{\partial\gamma_{p_j}})\sin^2(\gamma_{p_i}) &
\frac{\partial \eta_{p_{\color{blue}i}}}{\partial \gamma_{p_{\color{blue}{i}}}} = -(1-\eta_g-\sum_{k=1}^{i-1}\eta_{p_k})\sin^2(2\gamma_{p_i}) &
\text{i} \ne N_g \\
\\
\frac{\partial \eta_{p_{\color{brown}i}}}{\partial \gamma_{\color{brown}g}} = -(\frac{\partial\eta_g}{\partial\gamma_g}+\sum_{k=1}^{i-1}\frac{\partial\eta_{p_k}}{\partial\gamma_g}) &
\frac{\partial \eta_{p_{\color{brown}i}}}{\partial \gamma_{p{\color{brown}{j<i}}}} = -(\sum_{k=j}^{i-1}\frac{\partial\eta_{p_k}}{\partial\gamma_{p_j}}) & & 
\text{i} \equiv N_g \\
\end{array}



