---
number: 6
course: Metody Numeryczne
material: Instrukcja 6
author: Ł. Łaniewski-Wołłk
title: Zagadnienie własne
---

Z poprzednich zajęć wiemy, że równanie ruchu wygląda następująco:
\[M\ddot{x} = F - Sx\]
Policzmy ,,rozwiązanie ogólne równania jednorodnego''. Tzn: jakie funkcje $x=f(t)\phi$ spełniają równanie bez sił:
\[M\ddot{x} = - Sx\]
\[\ddot{f}(t)M\phi = - f(t)S\phi\]

Jeśli znajdziemy takie $\phi$, że:
$$\label{rownanie:wlasne}M\phi = \lambda S\phi$$
to otrzymamy:
\[\lambda\ddot{f}(t) = -  f(t) \quad\Rightarrow\quad f(t) = sin \left(t\frac{1}{\sqrt{\lambda}}\right)\]

To oznacza, że $sin(t\sqrt{\lambda})\phi$ jest oscylującym w czasie rozwiązaniem naszego równania dynamiki. Takie rozwiązanie nazywamy drganiem własnym układu. Równanie \eqref{rownanie:wlasne} nazywamy równaniem własnym.

Dziś skupimy się na znalezieniu zestawu wektorów $\phi$ i wartości $\lambda$ dla naszej belki


# Zacznijmy od największej $\lambda$
Zaczniemy od największej $\lambda$. Dobrze zauważyć, że największa wartość własna odpowiada najniższej częstotliwości. Są to drgania własne najmniej tłumione w fizycznym układzie i niosące zazwyczaj najwięcej energii w inżynierskich zastosowaniach.

Będziemy znajdywać nasz wektor $\phi$ iteracyjnie. Zauważmy, że wektor $\phi$ może być dowolnej długości. To znaczy: jeśli wektor $\phi$ spełnia równanie \eqref{rownanie:wlasne}, to także $2\phi$ go spełnia. Możemy więc arbitralnie wybrać ,,skale'' wektora $\phi$. Przyjmijmy, że $\phi^T M \phi = 1$, tzn: niesie on energię kinetyczną $\frac{1}{2}$.

Pomnóżmy równanie \eqref{rownanie:wlasne} przez $S^{-1}$. Otrzymamy:
\[\phi = \frac{1}{\lambda}S^{-1}M\phi\]
Na podstawie tego wzoru możemy skonstruować prostą iterację:
\begin{align*}
p &= S^{-1}M\phi\\
\phi &= p\frac{1}{\sqrt{p^TMp}}
\end{align*}
W pierwszym etapie liczymy wynik $S^{-1}M\phi$, a następnie go normalizujemy tak by $\phi^T M \phi = 1$. Jeśli odpowiednio długo będziemy wykonywać taką iterację, wektor własny odpowiadający największej wartości własnej zacznie dominować. Ostatecznie $\phi$ będzie składać się tylko z tego wektora, a $p^TMp$ zbiegnie do największej $\lambda$.


### Zadanie

Znajdź wektor $\phi$ odpowiadający największej wartości własnej wg. następującego schematu iteracji:
- Oblicz $b = M\cdot phi$
- Rozwiąż układ $S\cdot p = b$
- Oblicz $Mp = M\cdot p$
- Oblicz $phi = \frac{1}{\sqrt{\langle p, Mp \rangle}} p$



### Zadanie

Pokaż przemieszczenie $\phi$ przy pomocy funkcji `draw`. Zrób animację tego przemieszczenia przemnożonego przez $\sin{t}$.



### Zadanie
[Dla ciekawych]
By otrzymać bardziej płynną animację dodaj:\\
`static int pg=0; `\\
`setvisualpage(pg % 2);`\\
na początku funkcji `animate` w `winbgi2.cpp`. Zaś na końcu tej funkcji (przed  `return`):\\
`pg++;`\\
`setactivepage(pg % 2);`\\



# A teraz następne $\lambda$
Chcemy by wektory własne (drgania własne) były niezależne w energii kinetycznej. To znaczy, żeby energia kinetyczna ich sumy była równa sumie ich energii kinetycznych (,,$E_k(\phi_0+\phi_1) = E_k(\phi_0)+E_k(\phi_1)$''). To w połączeniu z naszą ,,skalą'' daje nam bardzo ważny warunek:
\[\begin{cases}
\phi_i^T M \phi_j = 0 &\quad \text{dla}\quad i\neq j \\
\phi_i^T M \phi_j = 1 &\quad \text{dla}\quad i = j \\
\end{cases}\]

Mówiąc językiem numeryki: wektory te są do siebie ortonormalne względem macierzy $M$. Takiej ortonormalizacji możemy dokonać znaną z Analizy Matematycznej metodą Grama-Schmidta:

\fbox{\begin{minipage}{8cm}
**Ortonormalizacja Grama-Schmidta**\\
Dla każdego $i$ od $1$ do $n$ wykonaj:
- dla każdego $i$ od $1$ do $i-1$ wykonaj (dla $i=1$ nic nie rób):
- Oblicz $\phi_i = \phi_i - \phi_j \langle \phi_j, M\phi_i \rangle$
- Oblicz $\phi_i = \frac{1}{ \sqrt{\langle \phi_i, M\phi_i \rangle}}\phi_i$
\end{minipage}}\\
\vspace{1cm}\\
Po tej procedurze wszystkie wektory $\phi$ są ortogonalne i długości $1$ względem macierzy $M$.


### Zadanie

Znajdź wektory $\phi_i$ odpowiadające $10$ciu największym wartościom własnym wg. następującego schematu iteracji:
- Oblicz $b = M\cdot phi_j$
- Rozwiąż układ $S\cdot p_j = b$
- Przepisz $phi_i = p_i$
- Wykonaj ortonormalizację G-S wektorów $phi$



### Zadanie

Zrób animację dla kolejnych przemieszczeń $\phi_i$ przemnożonych przez $\sin{t}$.



### Zadanie

Wyznacz odpowiednie $\lambda_i$



