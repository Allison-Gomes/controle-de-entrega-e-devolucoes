<h1 align="center"> Controle Logístico de Entregas e Devoluções </h1>


<h3> Entendimento do projeto: </h3>
<ul>
<li> Estudo de entregas, referente aos meses de junho e julho de 2023. Por ser os dois meses com maior criticidade nas entregas. Tendo o maior número de entregas feitas em atraso. </li>
<ol> Intuito do estudo: analisar a maior dificuldade, entre transportadoras e regiões. Visando melhorar os números e a satisfação dos clientes em 2024. </ol>
<li> Incluir uma aba informando as devoluções. </li>
<li> Dados fictícios, criados por Allison Gomes. </li>
</ul>

<div> <h3> Próximos passos </h3>
<ul>
<li> Documentação </li>
<ol> Definição: NOTION </ol>
<ol> Modelagem: LUCIDCHART </ol>
<ol> Banco de dados: SQL </ol>
<ol> Dashboard: Power BI </ol>
<li> Criar os relatórios no SQL e vincula-los </li>
<ol> Relatório das NFs </ol>
<ol> Relatório de Regiões </ol>
<li> Excel </li>
<ol> Relatório de Devoluções </ol>
<li> Vincular no Power BI e gerar apresentação </li>
</ul> </div>


<h4> Etapas descritas do Notion </h4>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/c8ca7fee-74a6-44af-a3b8-bc90f8d260cc)


<h4> Modelagem das tabelas: Lucidchart </h4>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/57def20a-dbce-46a7-91b2-066fdf66b116)


<h3> Banco de dados: SQL </h3>

<div><h4> Criação da tabela BASE DE NOTAS </h4>
CREATE TABLE [BASE DE NOTAS] ( <br>
[RAZAO SOCIAL TRANSPORTADOR] [VARCHAR] (150), <br>
[NOME FANTASIA] [VARCHAR] (100), <br>
[CNPJ TRANSPORTADOR] [CHAR] (14), <br>
[EMBARCADOR] [CHAR] (12), <br>
[CNPJ EMITENTE] [CHAR] (14), <br>
[CIDADE ORIGEM] [VARCHAR] (100), <br>
[UF ORIGEM] [CHAR] (2), <br>
[NRO NF] [VARCHAR] (10), <br>
[SERIE NF] [SMALLINT], <br>
[ROMANEIO] [CHAR] (15), <br>
[QTD VOLUMES] [VARCHAR] (5), <br>
[PESO] [FLOAT], <br>
[CUBAGEM] [FLOAT], <br>
[VALOR UNITARIO] [MONEY], <br>
[CNPJ CLIENTE] [CHAR] (14), <br>
[CLIENTE] [VARCHAR] (150), <br>
[CIDADE DESTINO] [VARCHAR] (100), <br>
[UF DESTINO] [CHAR] (2), <br>
[BAIRRO DESTINO] [VARCHAR] (100), <br>
[LOGRADOURO DESTINO] [VARCHAR] (150), <br>
[CEP DESTINO] [CHAR] (8), <br>
[DATA EMISSAO] [DATE], <br>
[DATA EMBARQUE] [DATE], <br>
[DATA INI. TRANSP.] [DATE], <br>
[PREVISÃO DE ENTREGA] [DATE], <br>
[DATA ENTREGA OPERAÇÃO] [DATE], <br>
[STATUS DE ENTREGA] [VARCHAR] (100), <br>
[COD. TRANSP.] [CHAR] (9) NOT NULL PRIMARY KEY, <br>
[MODAL] [VARCHAR] (10), <br>
[TIPO DE CARGA] [VARCHAR] (20), <br>
[CONDIÇÃO DE FRETE] [CHAR] (9), <br>
[NATUREZA DA MERCADORIA] [CHAR] (21), <br>
); <br> </div>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/540ec89b-197a-4314-8f6c-c2907b93eeb0)


<div> <h4> Criação da tabela REGIÕES <h4/>
CREATE TABLE [REGIOES] ( <br>
[SIGLA] [CHAR] (2) NOT NULL PRIMARY KEY, <br>
[REGIÃO] [VARCHAR] (12), <br>
[BRASIL + SIGLA] [CHAR] (11), <br>
[ESTADO] [VARCHAR] (25), <br>
[CAPITAL] [VARCHAR] (25), <br>
[LATITUDE] [FLOAT], <br>
[LONGITUDE] [FLOAT], <br>
); <br> </div>
  
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/6ed5c236-11af-466f-b8b6-2228a02a4b49)


<div> <h4> Input dos dados nas tabelas: <h4/>
<li> Base de notas </li>
<ol> Input automático </ol>
<ol> Baixar planilha (Excel Web) como .csv e vincular no SQL (Arquivo > Abrir > Arquivo = NovaBase3_SQL) </ol>
<ol> F5 </ol> </div>
  
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/e1d287a4-90de-4927-a6cc-400be34f5135)


<li> Regiões </li>
<ol> Input manual </ol>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/3b1cfb11-fa14-48b8-92b3-02db15d2a4eb)


<h4> Conferência da quantidade de linhas lançadas <h4/>
  
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/2f51234f-aaa6-4b0d-b8a0-b70c749e8a8e)


<h4> Desenho do esquema do banco de dados criado <h4/>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/1ab69070-0303-4115-adf9-8933f898bb8f)


<h4> Otimizando a visualização, alterando o nome de algumas colunas, e utilizando filtro <h4/>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/20a54eea-3189-4237-8510-1c63fdf392b0)


<h4> Efetuando a junção entre as tabelas BASE_DE_NOTAS e REGIOES (INNER JOIN) <h4/>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/1d5e539a-048a-438c-920c-6b967175d2d5) <br>

SELECT <br>
B.[NOME FANTASIA] AS [TRANSPORTADORA], <br>
B.[EMBARCADOR], <br>
B.[QTD VOLUMES] [VOLUMES], <br>
B.[PESO], <br>
B.[VALOR UNITARIO], <br>
B.[CLIENTE], <br>
B.[CIDADE DESTINO], <br>
R.[SIGLA] AS [UF], <br>
B.[STATUS DE ENTREGA], <br>
R.[REGIÃO], <br>
R.[BRASIL + SIGLA] AS [BR+SIGLA] <br>
FROM [BASE_DE_NOTAS] B <br>
INNER JOIN [REGIOES] R ON <br>
B.[UF DESTINO] = R.[SIGLA]; <br>


<h3> POWER BI </h3>
Tabela BASE_DE_NOTAS e REGIÕES importadas do SQL e tabela das Devoluções importadas diretamente do Excel <br>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/79de3e8d-66cd-48d5-b475-55a808ecb8b0)


<h4> Criando uma nova coluna, FATURAMENTO TOTAL, contemplando [peso * valor unitario] <h4/>

![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/632613c8-70b1-4baf-9420-9dfc39d62546)


<h4> Coluna criada para otimizar e melhorar a apresentação dos status das entregas <h4/>
  
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/ab3c9811-951d-42c0-94db-bd066c83c8df)


<div> <h4> Paleta de cores <h4/>
1° Cor: #12122B <br>
2° Cor: #383845 <br>
3° Cor: #5E5E5E <br>
4° Cor: #848478 <br>
5° Cor: #D3D3B9 <br> <br> </div>


<h3> Resultado Dashboard <h3/>
Link Power BI: <a href="https://app.powerbi.com/view?r=eyJrIjoiYmVlYWJlYTItMWQzYi00MjBkLTg4MjQtNzI1YjVkNjhmNTA3IiwidCI6IjlkOTQwNWRlLTYwNTctNDM2MS1hMTMwLWM0ZTZlYTdjMjk4MCJ9"> DASHBOARD </a><br>


![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/328d0764-908d-4cea-b76f-8a0efeced8db) <br/>
  
![image](https://github.com/Allison-Gomes/controle-de-entrega-e-devolucoes/assets/126164923/b79d6cb2-c51d-47d7-8351-69eb1c085529)

