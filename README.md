MesaSync | Dashboard de Análise de Vendas
Dashboard desenvolvido em Power BI, com dados demonstrativos de um restaurante, para acompanhar vendas e transformar registros de comandas e itens em indicadores de desempenho.
O projeto integra PostgreSQL, SQL, Power Query e DAX, com uma apresentação personalizada nas cores do MesaSync: azul escuro e laranja.
 
Os dados são fictícios e foram criados para fins de estudo e portfólio. Não representam resultados de um restaurante real.

Objetivo
Facilitar a leitura do desempenho comercial de um restaurante, permitindo consultar o faturamento, o volume de atendimentos e a composição das vendas em um período selecionado.
O relatório ajuda a responder perguntas como:
- Quanto o restaurante faturou no período?
- Quantas comandas foram concluídas?
- Qual foi o gasto médio por comanda?
- Quantos itens foram vendidos?
- Quais categorias geraram mais receita?
- Como o faturamento variou ao longo do tempo?
Indicadores
Indicador	O que representa	Exibição
Faturamento	Receita dos itens válidos de comandas fechadas	Moeda com duas casas decimais
Comandas fechadas	Quantidade de comandas concluídas	Número inteiro
Ticket médio	Faturamento dividido pela quantidade de comandas fechadas	Moeda com duas casas decimais
Itens vendidos	Quantidade de itens vendidos considerada pela medida	Número inteiro com separador de milhar


Os valores dependem do período e dos filtros aplicados ao relatório.
Páginas do relatório
01 · Visão geral
- Quatro cartões com os principais indicadores;
- Filtro de datas para selecionar o período de análise;
- Gráfico de linha com a evolução do faturamento;
- Gráfico de barras com o faturamento por categoria de produto;
- Notas sobre os critérios usados na análise.
02 · Guia de leitura
Página explicativa para apoiar a interpretação dos indicadores e dos critérios do relatório.
Regras de negócio
- O faturamento considera apenas comandas com status FECHADA;
- Itens com status CANCELADO são excluídos do faturamento;
- O ticket médio corresponde ao faturamento dividido pela quantidade de comandas fechadas.
Exemplo da medida de faturamento:
Faturamento =
CALCULATE(
    SUM(Vendas[valor_item]),
    Vendas[status_comanda] = "FECHADA",
    Vendas[status_item] <> "CANCELADO"
)
Dados e modelagem
Os dados foram importados do PostgreSQL por meio das views:
- vw_resumo_comandas: resumo das comandas;
- vw_vendas_analiticas: dados analíticos de vendas.
No Power BI, o modelo relaciona Vendas[id_comanda] a Comandas[id_comanda], com cardinalidade muitos para um. Essa estrutura conecta os registros de vendas às respectivas comandas.
As principais medidas DAX são Faturamento, Comandas Fechadas, Ticket Médio e Itens Vendidos.
Tecnologias utilizadas
Tecnologia	Aplicação no projeto
PostgreSQL	Armazenamento dos dados demonstrativos e disponibilização das views
SQL	Consulta e organização dos dados
Power Query	Importação e preparação dos dados no Power BI
DAX	Cálculo dos indicadores
Power BI Desktop	Modelagem e construção do relatório interativo
Git e GitHub	Versionamento e apresentação do projeto


Arquivos do repositório
- [MesaSync_Dashboard_PowerBI.pbix](./MesaSync_Dashboard_PowerBI.pbix): projeto do relatório para abrir no Power BI Desktop;
- [dashboard-visao-geral.png](./dashboard-visao-geral.png): imagem de apresentação da visão geral;
- README.md: documentação do projeto.
Como visualizar
1. Baixe o arquivo [`MesaSync_Dashboard_PowerBI.pbix`](./MesaSync_Dashboard_PowerBI.pbix).
2. Abra o arquivo no Power BI Desktop.
3. Explore a página 01 · Visão geral e altere o período de análise.
4. Consulte a página 02 · Guia de leitura para entender os indicadores.
Para atualizar os dados a partir da fonte, é necessário ter acesso ao banco PostgreSQL e às views utilizadas no projeto. Ajuste o servidor, o banco e as credenciais nas configurações da fonte de dados antes de atualizar. O script de criação do banco não está incluído neste repositório.
Aprendizados demonstrados
- Conexão entre banco relacional e ferramenta de visualização;
- Modelagem de dados com relacionamento entre vendas e comandas;
- Aplicação de regras de negócio em medidas DAX;
- Seleção de indicadores para análise de vendas;
- Construção de gráficos e filtros para exploração dos dados;
- Padronização de valores monetários e contagens;
- Organização visual com identidade do projeto e orientações de leitura.
Autor
Vitor de França Costa
LinkedIn · GitHub
