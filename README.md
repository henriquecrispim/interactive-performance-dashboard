# Dashboard Interativo para Análise de Performance Humana 🏃‍♂️📊

Este repositório armazena uma aplicação analítica reativa desenvolvida em Python no ambiente Google Colab. O sistema conta com um motor matemático integrado que simula planilhas complexas de treinamento de corrida de rua, tratando e exibindo dados de volume, ritmo (*pace*) e intensidade cardíaca por meio de componentes visuais 100% interativos.

## Como Funciona o Dashboard Interativo?
Diferente de relatórios estatísticos estáticos, este projeto responde dinamicamente a comandos do usuário em tempo real:
1. **Filtro Categórico (Widgets):** Um menu suspenso integrado captura as ações do usuário e realiza consultas assíncronas no banco de dados em memória via `ipywidgets`.
2. **Subplots Sincronizados (Plotly):** O pipeline processa e renderiza gráficos acoplados de alta fidelidade com aceleração de hardware. O eixo do ritmo (*pace*) é invertido matematicamente (`autorange="reversed"`) para respeitar a lógica analítica esportiva: quanto menor o tempo por quilômetro, mais rápido foi o estímulo e mais alto o ponto se posiciona no gráfico.

---

## Engenharia Algorítmica: Como os Dados Foram Gerados?

Para viabilizar o protótipo do painel sem depender de planilhas de terceiros, o projeto implementa um **Gerador de Dados Sintéticos Estruturados** utilizando distribuições probabilísticas e matemáticas via NumPy e Pandas. Os dados replicam perfeitamente o comportamento fisiológico e a rotina de um atleta de endurance real com base em três pilares lógicos:

### 1. Construção da Série Temporal de Treinos
O algoritmo inicializa definindo uma semente randômica fixa (`np.random.seed(42)`) para garantir a reprodutibilidade dos testes. Ele varre uma janela temporal de 12 semanas (84 dias). Para cada dia do calendário, o computador avalia uma função de probabilidade: há uma chance calibrada de **57%** de haver uma sessão de treino e **43%** de ser um dia de descanso/recuperação física, simulando uma frequência consistente de aproximadamente 4 treinos semanais.

### 2. Distribuição de Volume Baseada no Princípio 80/20
Ao determinar os dias com treino, o algoritmo escolhe o tipo de sessão aplicando pesos estatísticos rígidos baseados na metodologia científica de treinamento esportivo 80/20:
* **Rodagem (Z2):** 60% de probabilidade
* **Longo (Z2):** 15% de probabilidade
* **Intervalado (Z4/Z5):** 15% de probabilidade
* **Tempo Run (Z3):** 10% de probabilidade

Essa blocagem garante que **75% a 80% do volume total de treinos da série temporal pertençam à Zona 2** (aeróbica fundamental), simulando com precisão planilhas profissionais de preparação para maratonas e meia-maratonas.

### 3. Climatização Fisiológica Cruzada (If/Elif/Else)
Para que os dados tabulares possuam coerência científica em vez de gerarem números aleatórios absurdos, o gerador vincula as variáveis métricas através de limites específicos de distribuição uniforme para cada tipo de treino:
* **Treinos Intervalados (Tiros):** O script limita a distância para blocos curtos (6.0 a 10.0 km), mas força o ritmo (*pace*) a ser muito rápido ($4.2$ a $4.8$ decimal) e a frequência cardíaca média a atingir o limiar anaeróbico elevado (165 a 185 BPM).
* **Treinos Longos:** O script inverte a regra de engenharia, gerando alta quilometragem (14.0 a 22.0 km), associada a ritmos confortáveis e regenerativos ($5.5$ a $6.2$ decimal) e mantendo os batimentos cardíacos estritamente controlados na base aeróbica (130 a 145 BPM).

---

## Justificativa Teórica

### 1. Arquitetura de Software Orientada a Eventos no Caderno (Notebook)
O projeto implementa o conceito de funções de retorno (*callback functions*). Quando o valor do componente de seleção `Dropdown` se altera, uma rotina de fatiamento matricial limpa a memória do interpretador e re-renderiza as propriedades vetoriais do gráfico de forma isolada, demonstrando controle de concorrência e gerenciamento eficiente de memória em notebooks.

### 2. Prototipagem de Dados com Regras de Negócio
A habilidade de estruturar geradores de dados sintéticos complexos é um grande ativo na engenharia de dados. Ela permite que sistemas analíticos completos, painéis e modelos preditivos sejam construídos, testados e validados em arquitetura de código antes mesmo que sensores físicos, APIs corporativas ou bancos de dados reais de clientes estejam disponíveis.

---

## 🛠️ Tecnologias Utilizadas
* **Python 3**
* **IPyWidgets:** Construção de componentes visuais de interface e manipulação de eventos (*front-end* assíncrono no notebook).
* **Plotly Graph Objects:** Renderização de gráficos interativos com suporte a aceleração gráfica por hardware e ferramentas de *zoom* e *hover*.
* **Pandas & NumPy:** Geração distribuída e modelagem de séries temporais de desempenho.

---

## 📈 Resultados e Demonstração Operacional
Ao executar o pipeline no notebook, a aplicação inicializa exibindo o comportamento global acumulado de todas as sessões. O diferencial técnico reside no fato de o usuário poder utilizar os seletores para fatiar dinamicamente a base histórica.

Diferente de relatórios engessados, os gráficos gerados nesta solução permitem que o utilizador isole variáveis passando o cursor do mouse sobre os pontos para auditar metadados flutuantes, aproximar janelas específicas de semanas de treino (*zoom*) e ligar/desligar traços diretamente na legenda interativa.

---

## 🔍 Interpretação dos Resultados

A leitura do painel interativo permite realizar análises diagnósticas profundas de desempenho físico:

### 1. Diagnóstico de Eficiência Aeróbica (Pace vs BPM)
Ao isolar os treinos longos ("Longo (Z2)") no menu interativo, o analista consegue auditar a estabilidade cardiovascular. Se a linha de tendência do ritmo se mantiver linear ou descendente (ritmo mais rápido) enquanto a linha de barras da frequência cardíaca média se mantiver plana abaixo de zonas críticas, o sistema biológico modelado está evoluindo em sua base de resistência fundamental (adaptação mitocondrial).

### 2. Análise de Carga de Choque e Supercompensação
Ao filtrar por treinos "Intervalados", o painel destaca os picos extremos de frequência cardíaca e as reduções de tempo por quilômetro (*pace* de tiro). Cruzar o volume semanal desses blocos com os treinos subsequentes de rodagem leve serve para calcular o tempo necessário de recuperação (*recovery time*), mitigando riscos de lesão por overtraining e garantindo a aplicação correta dos estímulos de supercompensação.

---

## 🧠 Competências Demonstradas
* Desenvolvimento de interfaces interativas (*Graphical User Interfaces - GUI*) integradas a pipelines de análise de dados.
* Domínio na biblioteca Plotly para construção de narrativas visuais complexas e customizadas.
* Organização, modelagem matemática e tratamento avançado de séries temporais com múltiplas variáveis (*multivariate time-series*).

---

## 🚀 Como Executar o Projeto
1. Abra o arquivo com a extensão `.ipynb` deste repositório diretamente no seu **Google Colab**.
2. Execute todas as células pressionando as teclas **Ctrl + F9** (ou vá no menu superior em *Ambiente de Execução* -> *Executar tudo*).
3. O painel completo será renderizado no final do caderno de forma viva. Use o componente interativo de menu suspenso para selecionar os diferentes filtros e passe o ponteiro sobre as linhas e barras para ler as métricas detalhadas de performance.
