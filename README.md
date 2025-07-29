# 📊 Backtesting de Recomendações do ChatGPT na Bolsa de Valores

Este projeto realiza um levantamento estatístico para avaliar a eficácia do modelo de linguagem **ChatGPT (baseado no GPT-o3)** em fornecer recomendações de investimento (compra/venda) baseadas em análise técnica de gráficos de ações.

## 📝 Sobre o Projeto

A principal questão investigada foi: **Quão assertivo é um modelo de IA como o ChatGPT ao analisar um gráfico de ações e sugerir pontos de entrada, ganho (take profit) e perda (stop loss)?**

Para responder a essa pergunta, foi desenvolvida uma metodologia de backtesting onde o modelo de IA atuou como um "trader", tomando decisões exclusivamente com base nas informações visuais dos gráficos.

Foram escolhidas três ações de diferentes setores e com perfis de volatilidade distintos para o estudo:
*   **Tesla (TSLA)**
*   **Pfizer (PFE)**
*   **NVIDIA (NVDA)**

## ⚙️ Metodologia

O fluxo de trabalho do projeto foi dividido em quatro etapas principais:

1.  **Geração de Gráficos**: Para cada ação, foram gerados gráficos semanais seguindo um padrão visual consistente. Cada gráfico representava uma "fotografia" do mercado em um determinado momento, servindo como a única fonte de informação para a IA.

2.  **Análise e Recomendação pela IA**: Cada imagem de gráfico semanal foi submetida ao ChatGPT (modelo GPT-3). Foi solicitado ao modelo que realizasse uma análise técnica e fornecesse uma recomendação clara, contendo:
    *   Ponto de Entrada (se houvesse oportunidade de compra)
    *   Alvo de Ganho (Take Profit)
    *   Ponto de Stop (Stop Loss)
    
    O critério para identificar uma oportunidade de compra ou venda foi deixado **inteiramente a critério do modelo**, sem qualquer viés ou direcionamento humano.

3.  **Execução Simulada dos Trades**: As recomendações da IA foram utilizadas para simular operações de compra e venda. Cada trade executado foi registrado em um dataset, incluindo o ativo, os preços de entrada, stop, gain e o resultado final da operação.

4.  **Análise Estatística (Backtest)**: Com o dataset de trades consolidado, foi realizada uma análise estatística para medir o desempenho do modelo. Métricas como taxa de acerto, payoff, lucro/prejuízo por ativo e o desempenho geral foram calculados para quantificar a assertividade da IA.

## 📁 Estrutura do Projeto

O código-fonte está organizado em três Jupyter Notebooks principais, cada um responsável por uma etapa do processo:

*   `Gerador de gráficos.ipynb`
    *   **Responsabilidade**: Conectar-se a uma fonte de dados de mercado (ex: Yahoo Finance), baixar os dados históricos das ações e gerar as imagens dos gráficos no formato padronizado para análise da IA.

*   `Executando trades.ipynb`
    *   **Responsabilidade**: Simular a execução dos trades com base nas recomendações fornecidas pelo ChatGPT. Ele processa as saídas da IA, "abre" as operações e as "fecha" quando o preço atinge o alvo de ganho ou o stop, registrando tudo em um arquivo `.csv` ou similar.

*   `Backteste.ipynb`
    *   **Responsabilidade**: Carregar o dataset de trades gerado pelo notebook anterior e calcular as métricas de desempenho. É aqui que os resultados estatísticos são consolidados e visualizados, mostrando a taxa de acerto, o resultado financeiro simulado e outras estatísticas relevantes.

## 🛠️ Tecnologias Utilizadas

*   **Python 3.x**
*   **Jupyter Notebook**
*   **Pandas**: Para manipulação e análise dos dados.
*   **Matplotlib / Seaborn**: Para a geração dos gráficos.
*   **yfinance**: Para obter os dados históricos das ações.
*   **OpenAI API**: Para interagir com o modelo ChatGPT.

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure sua chave da API da OpenAI:**
    *   Crie um arquivo `.env` na raiz do projeto e adicione sua chave:
        ```
        OPENAI_API_KEY="sua-chave-aqui"
        ```
    *   O código deverá ser ajustado para ler esta variável de ambiente. **Nunca** publique sua chave diretamente no código.

4.  **Execute os notebooks na ordem correta:**
    1.  Execute o `Gerador de gráficos.ipynb` para criar as imagens.
    2.  Execute o `Executando trades.ipynb` para simular os trades com base nas recomendações (esta etapa pode exigir a interação manual com a API ou um script para automatizá-la).
    3.  Execute o `Backteste.ipynb` para analisar os resultados.

## 📈 Resultados

Os resultados detalhados da análise estatística, incluindo gráficos de desempenho e tabelas de métricas, podem ser encontrados no notebook `Backteste.ipynb`.

**Principal Conclusão:**
A conclusão fundamental do estudo é que, com base na amostragem e metodologia utilizadas, o uso do ChatGPT como um analista autônomo para recomendações de investimento **não se mostrou viável**.

*   **Assertividade**: O modelo apresentou uma taxa de acerto geral baixa, indicando que suas previsões baseadas em análise técnica visual não foram consistentemente precisas.
*   **Resultado Financeiro**: O backtest simulado resultou em um prejuízo líquido, demonstrando que seguir as recomendações da IA teria levado a perdas de capital no período e com os ativos analisados.

Apesar do resultado negativo em termos de viabilidade, o projeto serve como um importante estudo sobre as capacidades e limitações atuais dos modelos de linguagem em domínios especializados e de alta complexidade como o mercado financeiro.

---

### ⚠️ Aviso Legal

Este é um projeto de estudo e pesquisa de caráter puramente acadêmico e experimental. **As análises e recomendações geradas pela Inteligência Artificial não constituem, de forma alguma, aconselhamento financeiro.** O mercado de ações envolve riscos significativos de perda de capital. Não utilize as informações e resultados deste projeto como base para suas decisões de investimento reais. **Faça sua própria pesquisa (DYOR - Do Your Own Research).**
