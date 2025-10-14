OS OUTPUTS (GRÁFICOS) ESTÃO AQUI:


******** A maioria dos outputs são dinâmicos, o que não é possível visualizar no preview do gitHub, mas você pode baixar e executar no VSCode. Vou printar os resultados neste preview, mas a qualidade não é a mesma. Se houver algum ajuste que vocês queiram fazer, pode me mandar mensagem, sou bacana. Abs.,*********


**Sistema de Classificação Multidimensional para Análise de Investimentos**

Este sistema implementa uma metodologia quantitativa robusta para avaliação e ranking de empresas públicas brasileiras utilizando alguns pilares de análise fundamentalista.Basicamente, vou classificar as empresas que estão no Brasil, que são públicas, numa espécie que classificador para fins de investimento. Fiz tudo isso num final de semana, qualquer atualização, principalmente em função das premissas dos classificadores, farei assim que possível. O objetivo é só demonstrar as tecnicalidades do projeto e conhecimento a respeito dos demosntrativos e indicadores financeiros. Em resumo, o projeto foi desenvolvido para identificar oportunidades de investimento com base em dados obtidos do Capital IQ.

**1. METODOLOGIA DE CLASSIFICAÇÃO POR CLASSES**

Priorizei os dados a partir de 2022, já que em 2021 os dados ainda sofriam influências por conta da pandemia. Mas a composição da base de dados inclui 2021, se vocês quiserem que a análise reflita esses outliers, é possível alterar os parâmetros.

**1.1 class_CAGR (Crescimento)**
Métricas analisadas:
•	Revenue CAGR (2022-LTM)
•	EBITDA CAGR (2022-LTM)
•	Net Income CAGR (2022-LTM)

Critérios de classificação:

•	Excelente: ≥2 métricas com CAGR > 15%
•	Boa:       ≥ 2 métricas com CAGR > 5%
•	Ok:        ≥ 2 métricas com CAGR ≥ 0%
•	Ruim:      ≥ 2 métricas com CAGR < 0%
•	Péssima:   Demais casos
Empresas em trajetória de alto crescimento, potenciais candidatas para growth equity ou buy-and-build strategies
Boa: Crescimento consistente acima da inflação, adequadas para value creation através de melhorias operacionais
Ok/Ruim: Empresas maduras ou em dificuldades - requerem turnaround ou estratégias de consolidação
Péssima: Red flags significativos, risco de distress ou necessidade de reestruturação profunda

**1.2 class_Margins (Rentabilidade Operacional)**
Não considerei margem bruta, justamente para comparar maçãs com maçãs. Foquei em EBITDA e Lucro Líquido, que é o mais próximo do fluxo de caixa e do fluxo livre para o investidor de equity, respectivamente.
Métricas analisadas:
•	EBITDA Margin LTM
•	Net Margin LTM

Sistema de pontuação:

Cada métrica recebe de -2 a +2 pontos baseado em percentis. Score total determina classificação (≥3 = Excelente, ≥2 = Boa, etc.)

•	Excelente: Margens superiores indicam poder de precificação, vantagens competitivas ou eficiência operacional excepcional
•	Boa: Margens saudáveis com espaço para expansão através de operational excellence
•	Ok: Margens medianas - foco em cost optimization e efficiency gains
•	Ruim/Péssima: Estrutura de custos insustentável, necessidade de reestruturação operacional urgente
•	Value Driver: Margens são proxy de qualidade do modelo de negócio e resiliência competitiva.

**1.3 class_Multiplos (Valuation)**
Aqui, há uma certa complexidade técnica, porque é uma métrica que depende do setor. Acho que todas as métricas, em geral, dependem do setor. Mas no final do dia, o que importa é fluxo de caixa para os shareholders. 
Metodologia diferenciada: Comparação relativa à mediana do setor, usei múltiplos de Enterprise Value e Equity Value.

Múltiplos avaliados:
•	EV/Revenue
•	EV/EBITDA LTM
•	P/E LTM
•	P/BV LTM
Sistema de scoring:
Para cada múltiplo:
•	- ≤70% da mediana setorial:  +2 pontos (significativo desconto)
•	- ≤85% da mediana:            +1 ponto  (desconto moderado)
•	- ±15% da mediana:             0 pontos (fair value)
•	- ≤130% da mediana:           -1 ponto  (prêmio moderado)
•	- >130% da mediana:           -2 pontos (prêmio excessivo)
•	Score total: -6 a +6

**Classificação final:**
•	    Excelente: ≥4 pontos (oportunidade de valor significativa);
•	    Boa: ≥2 pontos (valuation atrativo) 
•	    Ok: ≥-1 ponto (fair value) 
•	    Ruim: ≥-3 pontos (overvalued) 
•	    Péssima: <-3 pontos (extremamente caro).

•	    Excelente: Potenciais mispriced assets - candidatos ideais para leveraged buyouts com upside múltiplo na entrada
•	    Boa: Entry point atrativo com múltiplo de entrada baixa aumentando IRR potencial
•	    Ok: Valuation justo - retorno dependerá de value creation operacional
•	    Ruim/Péssima: Valuation proibitivo - dificuldade em gerar retornos adequados ao risco mesmo com melhorias operacionais
•	    Vantagem metodológica: Comparação setorial elimina distorções de múltiplos absolutos (ex: tech tem P/E naturalmente alto vs utilities). Foca em relative value dentro de comps relevantes.

**1.4 class_Qualidade (Saúde Financeira):**
É uma métrica importante, reflete o peso da estrutura de capital. Obviamente empresas muito envidadas em relação aos peers, devem sofrer redução no valor do equity.
Métricas analisadas:
•	Debt/EBITDA LTM (alavancagem)
•	Interest Coverage LTM (capacidade de serviço da dívida)
•	Levered FCF Margin LTM (geração de caixa pós-dívida)

Classificação:

•	Excelente: ≥4 (balanço forte, baixa alavancagem)
•	Boa:       ≥2 (estrutura de capital saudável)
•	Ok:        ≥0 (alavancagem gerenciável)
•	Ruim:      ≥-2 (stress financeiro moderado)
•	Péssima:   <-2 (risco de distress)
        Obs.: Empresas com Debt/EBITDA < 3x e Interest Coverage > 5x permitem estruturas de capital mais agressivas.

**1.5 class_Profitability (Retorno sobre Capital)**
Métricas analisadas:
•	ROE LTM (retorno sobre patrimônio)
•	ROA LTM (retorno sobre ativos)
•	Current Ratio LTM (liquidez de curto prazo)
•	Asset Turnover LTM (eficiência de ativos)
Classificação:
•	Excelente: ≥5 (retornos excepcionais sobre capital) 
•	Boa: ≥2 (retornos acima do custo de capital) 
•	Ok: ≥0 (retornos adequados) 
•	Ruim: ≥-3 (destruição de valor) 
•	Péssima: <-3 (ineficiência severa de capital)

**Interpretação:****
•	Excelente: ROE > 20% indica vantagens competitivas sustentáveis
•	Boa: Retornos adequados com espaço para melhorias via operational excellence e working capital optimization.
•	Ok: Foco em ROIC improvement através de asset light strategies e efficiency programs.
•	Ruim/Péssima: Asset-heavy businesses com retornos subótimos - candidatos para sale-leaseback, divestitures ou operational turnaround.
Asset Turnover: Métrica crítica para identificar eficiência operacional. Baixo turnover com margens altas = pricing power. Alto turnover com margens baixas = volume business.

**1.6 class_Dividends**
Metodologia avançada: Análise histórica de 5 anos (FY2021-LTM)
Dimensões avaliadas:

1.	Yield Médio Histórico: 
•	Média dos dividend yields (dividendos/preço) nos últimos anos
•	Pontuação: ≥5% (+2), ≥3% (+1), ≥1.5% (0), <1.5% (-1).
2.	Consistência: 
•	Número de anos com pagamento de dividendos
•	Pontuação: ≥4 anos (+2), ≥3 anos (+1), ≥2 anos (0), <2 (-1)
3.	Sustentabilidade (Payout Ratio): 
•	Payout médio histórico
•	Pontuação: ≤60% (+1), ≤80% (0), >80% (-1)
4.	Crescimento: 
•	Comparação dividendos recentes vs antigos.
•	Pontuação: >10% growth (+1), >0% (0), negativo (-1).

**Classificação:**
•	Excelente: ≥5 (dividend aristocrat quality) bacana esse termo, né?;
•	Boa:       ≥3 (pagador consistente);
•	Ok:        ≥0 (dividendos ocasionais);;
•	Ruim:      ≥-2 (inconsistência);
•	Péssima:   <-2 (sem histórico ou payout insustentável).

•	Excelente: Empresas maduras com FCF consistente
•	Boa: Cash generation confiável
•	Ok: Flexibilidade para redirecionar capital de dividendos para growth capex ou M&A;
•	Ruim/Péssima: Red flag sobre FCF generation ou a empresa usa caixa para investir na própria operação.

Empresas com histórico sólido de dividendos indicam FCF confiável - permitindo dividend recaps que podem retornar 30-50% do equity investment em 2-3 anos enquanto ainda se mantém ownership.
Payout Ratio < 60%: Indica espaço para aumentar dividendos ou reinvestir em crescimento, ambos positivos para value creation.

**
**2. COMPOSITE SCORE: INTEGRAÇÃO MULTIDIMENSIONAL****
**2.1 Metodologia de Agregação**
Ponderação igualitária, atribuí o mesmo peso para cada uma das classes, mas, novamente, se for do interesse dos senhores, é possível alterar. Particularmente, esse é só um critério que eu uso para investimentos em equity, existem muitos outros que não podem ser quantifidcados. 
composite_score = (
    class_CAGR_score * 1.0 +
    class_Margins_score * 1.0 +
    class_Multiplos_score * 1.0 +
    class_Qualidade_score * 1.0 +
    class_Profitability_score * 1.0 +
    class_Dividends_score * 1.0
)

**Racional**: Pesos iguais evitam overweighting de qualquer dimensão específica, permitindo que empresas com diferentes perfis sejam avaliadas holisticamente.

Range do score: -12 a +12

Classificação final:

•	Excelente: ≥8  (top quartile - high conviction opportunities)
•	Boa:       ≥4  (above median - attractive risk/reward)
•	Ok:        ≥-2 (median - selective opportunities)
•	Ruim:      ≥-7 (below median - high risk)
•	Péssima:   <-7 (bottom quartile - avoid)

Cara, eu fiquei surpreso com o resultado dessa análise, a melhor empresa foi uma que eu nem conhecia. Eu imaginava uma WEG da vida, um Banco do Brasil.


<img width="1799" height="792" alt="image" src="https://github.com/user-attachments/assets/33498e6b-8663-4543-b6d6-21880e11fbbe" />
<img width="1766" height="369" alt="image" src="https://github.com/user-attachments/assets/812bcf74-867c-4563-a76b-f3f6f3bfc002" />

<img width="1759" height="833" alt="image" src="https://github.com/user-attachments/assets/db68a2ee-83eb-4cc2-acc5-a5c92725e7d3" />

<img width="1771" height="871" alt="image" src="https://github.com/user-attachments/assets/f805078e-f8b4-4d6f-a63c-cfdca2d78c2c" />

<img width="1761" height="687" alt="image" src="https://github.com/user-attachments/assets/62cc3edf-6bd3-40b0-8bc8-70a74c20e6fc" />

<img width="1769" height="883" alt="image" src="https://github.com/user-attachments/assets/5c9e13c3-0032-45cb-a17f-71bb43ecbcb4" />


<img width="1764" height="868" alt="image" src="https://github.com/user-attachments/assets/7939696d-55d2-4e65-b19f-f5a1cdb87fc1" />



<img width="1748" height="588" alt="image" src="https://github.com/user-attachments/assets/21ebfb38-c97b-43c0-9ed6-94df25081269" />


<img width="980" height="687" alt="image" src="https://github.com/user-attachments/assets/87fee7e4-3e6d-440f-92fc-ef7925334aec" />


<img width="976" height="681" alt="image" src="https://github.com/user-attachments/assets/86346184-8cfb-4462-9af1-d830f8091754" />



<img width="1512" height="853" alt="image" src="https://github.com/user-attachments/assets/809cd0e4-ab50-4eea-b0bd-b290c2ab6745" />



<img width="1770" height="599" alt="image" src="https://github.com/user-attachments/assets/f2675c92-2d42-4f8f-aac6-b1c8493cfbe3" />



**CONCLUSÃO**
Este projeto fornece uma metodologia sistemática, replicável e objetiva para screening e análise de oportunidades de investimento. A abordagem multi-pilar captura diferentes dimensões de qualidade empresarial, enquanto a comparação setorial garante que o valuation e as métricas de performance são contextualizadas apropriadamente.
O sistema serve como:
Invesstment sourcing tool: Identificação rápida de high-quality targets;
Due diligence framework: Estrutura para deep dives setoriais;
Value creation roadmap
Portfolio monitoring dashboard: Tracking sistemático de performance vs benchmarks;

**Próximos passos:**
Não sei, podemos aplicar mais modelos estatísticos ou machine learning. A princípio, esse projeto seria puramente para redes neurais, mas aplicando para teses de investimentos, parece um pouco simplista, principalmente depois de ler Human Action. Estamos a frente.
Abs.,

