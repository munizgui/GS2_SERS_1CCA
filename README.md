# Citizen Assist AI — Soluções em Energias Renováveis e Sustentáveis

> **Disciplina:** Soluções em Energias Renováveis e Sustentáveis (SERS)  
> **Curso:** Ciência da Computação — Turma 1CCA (FIAP — Global Solution 2026.2)

## 👥 Integrantes do Grupo
* **Guilherme Lopes Muniz** — RM: 569521
* **Gustavo Russo Balizardo** — RM: 569283

## 🎯 1. Público-Alvo e Necessidade Energética
* **Público escolhido:** Famílias residenciais urbanas de baixa e média renda (região metropolitana de São Paulo/SP) que enfrentam custos elevados na fatura de energia elétrica.
* **Necessidade abordada:** Falta de orientação clara e acessível para identificar desperdícios domésticos (como uso prolongado de chuveiro elétrico e equipamentos em *stand-by*) e avaliar financeiramente se vale a pena investir em eficiência energética ou energia solar.
* **Contribuição ao Citizen Assist AI:** O assistente integra um motor de cálculo em Python (`citizen_assist_ai_energia.ipynb`) que traduz dados técnicos (kW, kWh, tarifa, irradiação solar, payback e emissões de CO₂) em recomendações personalizadas conforme o perfil do imóvel do cidadão.

## 📊 2. Análise de Consumo, Dados e Premissas
Os dados reais foram separados das premissas adotadas para o cenário de referência:

### Dados Públicos (Fontes Verificáveis)
* **Tarifa média residencial (SP):** R$ 0,85/kWh (estimativa com impostos; fonte: ANEEL).
* **Irradiação solar média diária em São Paulo:** 4,45 kWh/m²/dia (fonte: CRESESB / INPE).
* **Fator de emissão do Sistema Interligado Nacional (SIN):** 0,0385 kg CO₂/kWh (fonte: MCTI).
* **Peso típico do chuveiro elétrico:** 25% a 35% do consumo residencial (fonte: EPE / PROCEL).

### Premissas Estimadas (Caso Base: Família de 4 pessoas)
* **Consumo mensal atual:** 350 kWh/mês (4.200 kWh/ano) → Custo de **R$ 297,50/mês** (**R$ 3.570,00/ano**).
* **Carga crítica identificada:** Chuveiro de 5.500 W ligado por 40 min/dia ≈ 110,5 kWh/mês.
* **Horizonte de comparação:** 12 meses (curto prazo) e 5 anos (médio prazo), sem inflação energética.
* **Custo de disponibilidade:** 50 kWh/mês (taxa mínima da rede considerada no dimensionamento solar conforme Lei 14.300/2022).

## ⚖️ 3. Cálculos e Comparação das Alternativas

Comparação aplicada ao mesmo consumo base (**350 kWh/mês**):

1. **Alternativa 1 — Eficiência Energética e Mudança de Hábitos:** Troca de lâmpadas por LED, redução de *stand-by* e ajuste de potência/tempo de banho (economia estimada de **75 kWh/mês** ou **900 kWh/ano**).
2. **Alternativa 2 — Fonte Renovável (Solar Fotovoltaica On-Grid de 2,2 kWp):** 4 módulos de 550 Wp com *Performance Ratio* de 0,78 (`2,2 kWp × 4,45 h × 30 dias × 0,78 ≈ 229 kWh/mês` ou **2.748 kWh/ano**).

| Critério Comparativo | Cenário Base (Atual) | Alt. 1: Eficiência Energética | Alt. 2: Solar Fotovoltaica (2,2 kWp) |
| :--- | :--- | :--- | :--- |
| **Investimento Inicial** | R$ 0,00 | R$ 250,00 | R$ 8.800,00 |
| **Energia Poupada / Gerada** | 0 kWh/ano | 900 kWh/ano | 2.748 kWh/ano |
| **Economia Financeira Anual** | R$ 0,00 | R$ 765,00/ano | R$ 2.335,80/ano (líquida c/ Fio B) |
| **Tempo de Retorno (Payback)** | - | ~4 meses | ~3,8 anos |
| **Saldo Líquido em 5 Anos** | -R$ 17.850,00 (gasto) | +R$ 3.575,00 de economia | +R$ 2.879,00 de lucro líquido |
| **CO₂ Evitado (5 anos)** | 0 kg CO₂ | 173,25 kg CO₂ | 529,00 kg CO₂ |
| **Viabilidade** | Imediata | **Alta:** casas e apartamentos | **Média:** exige telhado próprio sem sombra |

## 💡 4. Justificativa das Recomendações e Limitações
* **Recomendação Híbrida:** O assistente orienta começar imediatamente pela **Eficiência Energética** (baixo investimento e retorno rápido) e, caso o usuário possua telhado próprio disponível, investir na **Energia Solar Fotovoltaica** para redução de ~65% da fatura e ganho ambiental expressivo ao longo de 25 anos de vida útil.
* **Condições e Limitações (Explícitas nas respostas do assistente):**
  * Os valores são **estimativas** educacionais e não garantias financeiras.
  * A geração solar depende de sombreamento, orientação/inclinação do telhado e sazonalidade climática.
  * A economia financeira está sujeita às regras da Lei 14.300/2022 (cobrança gradual do Fio B) e bandeiras tarifárias da ANEEL.

## 🧪 5. Registro de Testes com Usuários e Ajustes Realizados

| ID | Perfil Testado (Anonimizado) | Pergunta Enviada | Feedback Recebido | Ajuste Implementado |
| :--- | :--- | :--- | :--- | :--- |
| **T01** | Morador de casa própria (350 kWh/mês) | *"Vale mais a pena mudar hábitos ou pôr painel solar?"* | Achou o termo *"Performance Ratio"* muito técnico. | Linguagem simplificada nas respostas do assistente. |
| **T02** | Moradora de apartamento alugado (220 kWh/mês) | *"Moro de aluguel em prédio, como baixar minha conta?"* | Primeira versão sugeriu painel solar no telhado. | Inclusão do parâmetro `possui_telhado_proprio` para filtrar viabilidade. |
| **T03** | Estudante universitário | *"A economia da energia solar é garantida todo mês?"* | Dúvida sobre dias nublados e taxas mínimas. | Adição do bloco obrigatório de **Condições e Limitações**. |
| **T04** | Pequeno comerciante (500 kWh/mês) | *"De onde saíram os valores da tarifa e do CO₂?"* | Pediu transparência sobre a origem dos dados. | Exibição automática das fontes oficiais em todas as respostas. |

## 🚀 6. Como Executar e Testar
1. Abra o notebook [`citizen_assist_ai_energia.ipynb`](./citizen_assist_ai_energia.ipynb) diretamente pelo GitHub ou clique em **Open in Colab**.
2. Execute todas as células (**Ambiente de execução > Executar tudo**).
3. *(Opcional)* Para testar com a LLM generativa ativa, adicione sua chave `GEMINI_API_KEY` nos **Segredos** do Google Colab. Sem a chave, o código executa automaticamente o modo determinístico validado.

## 📚 7. Referências Verificáveis
* **ANEEL:** Ranking de Tarifas Residenciais e Lei nº 14.300/2022 (`https://www.gov.br/aneel`)
* **CRESESB / INPE:** Atlas Brasileiro de Energia Solar — SunData (`http://www.cresesb.cepel.br`)
* **EPE / PROCEL:** Balanço Energético Nacional (`https://www.epe.gov.br`)
* **MCTI:** Fatores Médios de Emissão de CO₂ do SIN (`https://www.gov.br/mcti`)
