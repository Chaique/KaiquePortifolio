A Análise de Deviance (ANODEV) ou Análise do Desvio é uma generalização da ANOVA para modelos GLM, a partir de uma sequência de modelos encaixados (modelos da mesma família) os efeitos de covariáveis, de fatores e suas interações. [[Função Desvio ou Deviance]]
## Definição
Seja $M_{p1},\cdots,M_{p}$ uma sequência de modelos encaixados (obtidos por alguma restrição nos parâmetros) com parâmetros $p_{1}$<$p_{2}$ <$\cdots < p_{r}$, com matriz de modelos $X_{p1},...,M_{p}$ e desvios $D_{p1},\cdots,D_{p}$.
Observa-se que essas desigualdades entre as deviances, em geral, não se verifica a estatística de Pearson generalizada e, por essa razão, a comparação de modelos encaixados é ralizada, principalmente, baseada na função deviance.



<


$<$

$/<$
$\<$
${<}$



### Exemplo
Vamos supor um experimento inteiramente ao acaso realizado num esquema fatorial, com dois fatores A e B com $r$ repetições, sendo que os fatores A e B possuem $a$ e $b$ níveis.

Diz-se que dois termos A e B são ortogonais se a redução que A (ou B) causa na deviance $D_p$ é a mesma, esteja B (ou A) incluído, ou não, em um modelo.

Em geral, para os GLMs ocorre a não-ortogonalidade dos termos e a interpretação da tabela ANODEV é mais complicada do que a ANOVA usual.

## Tabela ANODEV

| Preditor Linear | g.l.          | Deviance       | Dif. de Deviance | Dif. de g.l. | Significado                  |
| --------------- | ------------- | -------------- | ---------------- | ------------ | ---------------------------- |
| Nulo            | rab-1         | $D_1$          | $D_1$            |              | Sem A                        |
| A               | a(rb-1)       | $D_A$          | $D_1-D_A$        | a-1          | A incluído B                 |
| A+B             | a(rb-1)-(b-1) | $D_{A+B}$      | $D_A-D_{A+B}$    | b-1          | B incluído A                 |
| A+B+AB          | ab(r-1)       | $D_{A\cdot B}$ | $D_{A\cdot B}$   | (a-1)(b-1)   | Interação AB incluídos A e B |
| Saturado        | 0             | 0              |                  | ab(r-1)      | Residuals                    |

Sejam os modelos encaixados $M_{p}$ e $M_{q}$ ($M_p$C$M_q$, $p<q$) parâmetros.

A estatística $D_p-D_q$ com ($q-p$) graus de liberdade, é interpretada como uma medida de variação dos dados, explicada pelos termos que estão em $M_q$ e não estão $M_p$, incluídos os efeitos dos termos em $M_p$.

Para $\phi$ conhecido, temos, assintoticamente, que:
$$
S_p-S_q=\phi^{-1}(D_p-D_q)\sim \chi^2_{q-p}
$$
onde:
- $S_p-S_q$: é igual à razão de verossimilhança.

Para $\phi$ desconhecido, deve-se uma estimativa $\hat{\phi}$ consistente, e a inferência pode ser baseada na estatística F, dada por:
$$
F=\frac{\frac{(D_p-D_q)}{(q-p)}}{\hat{\phi}}\sim F_{q-p;n-q}
$$
onde:
- $p$: números de parâmetros do modelo menor
- $q$: número de parâmetros do modelo maior
- $n$: número de variáveis $y$.
- F segue distribuição F de Snedecor.
- F segue distribuição F exata no modelo clássico, [[Teste Regressão Múltipla F-sequencial]].
## R
```r
anova(modelo_nulo,modelo1,test="Chisq")
#ou
anova(modelo,test = "Chisq")
#ou
avona(modelo)
```

