Controle Logístico de Entregas e Devoluções

Entendimento do projeto: <br/>
• Estudo de entregas, referente aos meses de junho e julho de 2023. Por ser os dois meses com maior criticidade nas entregas. Tendo o maior número de entregas feitas em atraso. <br/>
	• Intuito do estudo: analisar a maior dificuldade, entre transportadoras e regiões. Visando melhorar os números e a satisfação dos clientes em 2024. <br/>
• Incluir uma aba informando as devoluções. <br/>
• Dados fictícios, criados por Allison Gomes. <br/>
	
Etapas descritas do Notion
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/c8ca7fee-74a6-44af-a3b8-bc90f8d260cc)

• Documentação
	Definição: Notion
	Modelagem: Lucidchart
	Banco de dados: SQL
	Dashboard: Power BI
• Criar os relatórios no SQL e vincula-los
	Relatório das NFs
	Relatório de Regiões
• Excel
	Relatório de Devoluções
• Vincular no Power BI e gerar apresentação

• Modelagem das tabelas: Lucidchart
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/57def20a-dbce-46a7-91b2-066fdf66b116)


Banco de dados: SQL
• Criação da tabela BASE DE NOTAS
CREATE TABLE [BASE DE NOTAS] (
[RAZAO SOCIAL TRANSPORTADOR] [VARCHAR] (150),
[NOME FANTASIA] [VARCHAR] (100),
[CNPJ TRANSPORTADOR] [CHAR] (14),
[EMBARCADOR] [CHAR] (12),
[CNPJ EMITENTE] [CHAR] (14),
[CIDADE ORIGEM] [VARCHAR] (100),
[UF ORIGEM] [CHAR] (2),
[NRO NF] [VARCHAR] (10),
[SERIE NF] [SMALLINT],
[ROMANEIO] [CHAR] (15),
[QTD VOLUMES] [VARCHAR] (5),
[PESO] [FLOAT],
[CUBAGEM] [FLOAT],
[VALOR UNITARIO] [MONEY],
[CNPJ CLIENTE] [CHAR] (14),
[CLIENTE] [VARCHAR] (150),
[CIDADE DESTINO] [VARCHAR] (100),
[UF DESTINO] [CHAR] (2),
[BAIRRO DESTINO] [VARCHAR] (100),
[LOGRADOURO DESTINO] [VARCHAR] (150),
[CEP DESTINO] [CHAR] (8),
[DATA EMISSAO] [DATE],
[DATA EMBARQUE] [DATE],
[DATA INI. TRANSP.] [DATE],
[PREVISÃO DE ENTREGA] [DATE],
[DATA ENTREGA OPERAÇÃO] [DATE],
[STATUS DE ENTREGA] [VARCHAR] (100),
[COD. TRANSP.] [CHAR] (9) NOT NULL PRIMARY KEY,
[MODAL] [VARCHAR] (10),
[TIPO DE CARGA] [VARCHAR] (20),
[CONDIÇÃO DE FRETE] [CHAR] (9),
[NATUREZA DA MERCADORIA] [CHAR] (21),
);
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/540ec89b-197a-4314-8f6c-c2907b93eeb0)


• Criação da tabela REGIÕES
CREATE TABLE [REGIOES] (
[SIGLA] [CHAR] (2) NOT NULL PRIMARY KEY,
[REGIÃO] [VARCHAR] (12),
[BRASIL + SIGLA] [CHAR] (11),
[ESTADO] [VARCHAR] (25),
[CAPITAL] [VARCHAR] (25),
[LATITUDE] [FLOAT],
[LONGITUDE] [FLOAT],
);
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/6ed5c236-11af-466f-b8b6-2228a02a4b49)


Input dos dados nas tabelas:
• Base de notas
	Input automático
Baixar planilha (Excel Web) como .csv e vincular no SQL (Arquivo > Abrir > Arquivo = NovaBase3_SQL)
F5
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/e1d287a4-90de-4927-a6cc-400be34f5135)


• Regiões 
	Input manual
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/3b1cfb11-fa14-48b8-92b3-02db15d2a4eb)


Conferência da quantidade de linhas lançadas
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/2f51234f-aaa6-4b0d-b8a0-b70c749e8a8e)


Desenho do esquema do banco de dados criado
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/1ab69070-0303-4115-adf9-8933f898bb8f)


Otimizando a visualização, alterando o nome de algumas colunas, e utilizando filtro
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/20a54eea-3189-4237-8510-1c63fdf392b0)


Efetuando a junção entre as tabelas BASE_DE_NOTAS e REGIOES (INNER JOIN)
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/1d5e539a-048a-438c-920c-6b967175d2d5)
SELECT
B.[NOME FANTASIA] AS [TRANSPORTADORA],
B.[EMBARCADOR],
B.[QTD VOLUMES] [VOLUMES],
B.[PESO],
B.[VALOR UNITARIO],
B.[CLIENTE],
B.[CIDADE DESTINO],
R.[SIGLA] AS [UF],
B.[STATUS DE ENTREGA],
R.[REGIÃO],
R.[BRASIL + SIGLA] AS [BR+SIGLA]
FROM [BASE_DE_NOTAS] B
INNER JOIN [REGIOES] R ON
B.[UF DESTINO] = R.[SIGLA];


POWER BI
Tabela BASE_DE_NOTAS e REGIÕES importadas do SQL e tabela das Devoluções importadas diretamente do Excel
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/79de3e8d-66cd-48d5-b475-55a808ecb8b0)


Criado uma nova coluna, FATURAMENTO TOTAL, contemplando [peso * valor unitario]
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/632613c8-70b1-4baf-9420-9dfc39d62546)


Coluna criada para otimizar e melhorar a apresentação dos status das entregas
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/ab3c9811-951d-42c0-94db-bd066c83c8df)


Definição da paleta de cores
1° Cor: #12122B
2° Cor: #383845
3° Cor: #5E5E5E
4° Cor: #848478
5° Cor: #D3D3B9


Resultado Dashboard
https://app.powerbi.com/view?r=eyJrIjoiYmVlYWJlYTItMWQzYi00MjBkLTg4MjQtNzI1YjVkNjhmNTA3IiwidCI6IjlkOTQwNWRlLTYwNTctNDM2MS1hMTMwLWM0ZTZlYTdjMjk4MCJ9
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/3e2f031c-23b7-479e-a7ef-fe2b29366189)

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/607c11ed-b8bf-42e9-8a5e-b59c55f0fc29)
