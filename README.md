# DAX-Power-BI
Modelagem e Transformação de dados com DAX com Power BI

O objetivo deste projeto é modelar e transformar dados usando a linguagem DAX (Data Analysis Expressions) com o Microsoft Power BI. O DAX é uma linguagem poderosa que permite aos usuários criar fórmulas e expressões personalizadas para manipular e analisar dados. Este projeto guiará os usuários pelas etapas básicas de modelagem e transformação de dados com DAX no Power BI, incluindo a criação de medidas, cálculos e tabelas calculadas.

O processo consiste na criação das tabelas com base na tabela original. A partir da cópia serão selecionadas as colunas que irão compor a visão da nova tabela. Sendo assim, a partir da tabela principal serão criadas as tabelas:

Financials_origem (modo oculto – backup)

D_Produtos (ID_produto, Produto, Média de Unidades Vendidas, Médias do valor de vendas, Mediana do valor de vendas, Valor máximo de Venda, Valor mínimo de Venda)

D_Produtos_Detalhes(ID_produtos, Discount Band, Sale Price, Units Sold, Manufactoring Price)

D_Descontos (ID_produto, Discount, Discount Band)

D_Detalhes (*)
*Verifique as informações que não foram contempladas nas demais tabelas dimensão que fornecem maiores detalhes sobre vendas.

D_Calendário – Criada por DAX com calendar()

F_Vendas (SK_ID , ID_Produto, Produto, Units Sold, Sales Price, Discount Band, Segment, Country, Salers, Profit, Date (campos))


Passo 01 – Criação das tabelas dimensões
Foram criadas 5 tabelas dimensões e 1 tabela fato, derivadas da tabela "financials_origem". As tabelas são descritas a seguir:


![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/5a8dc3d3-00bc-4cc6-a926-e29d78e78fa8)


D_Produtos

Tabela dimensão criada para persistir valores agregados de vendas e medidas estatísticas. Possui os atributos "id_produto", "Product", Soma de Unidades Vendidas", "Valor Mín de Venda", "Valor Máx de Venda", "Média do Valor de Venda", "Mediana do Valor de Venda" e "Média da Manufatura". Foi realizado algumas funções DAX para realização de medidas. O atributo "id_produto" foi criado a partir da funcionalidade 'Tabela Índice' após a agregação.


![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/0ac42aab-14a3-4e62-84e0-94d65414a94a)

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/4c2f2864-8d1b-41af-a36a-0cb144f80eab)


D_Detalhes

Tabela dimensão criada para detalhar informações adicionais da tabela fato. 

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/c2bd1ab4-c964-484e-92e4-9167c682094c)


D_Data

A Tabela dimensão data foi criada a partir da data base e usada a fórmula DAX para criação das demais.

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/5fc16939-2690-4414-8c67-fa77c4f15955)

Exemplo:
WEEK NUMBER = WEEKNUM('D_Calendar'[Date])
MONTH = FORMAT(DATE(1, 'D_Calendar'[MONTH NUMBER],1), "MMM")


D_Produto_Detalhes

Tabela Dimensão persistida para classificação dos dados da tabela fato. Formada atributos da base para detamento sobre o produtoção.
![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/d7fc7418-3bdb-42d0-90b5-3128f0174c01)


D_Desconto

Tabela Dimensão com a função de referenciar os descontos "Discounts" e a faixa de desconto "Discounts Band". 

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/4b18731f-6f7e-4280-9533-28dc9c06f599)


F_Vendas

Por fim, a tabela fato que carrega a chave  "SK_id" (surrogate key). A tabela também carrega consigo alguns atributos únicos "Units Sold", "Sale Price", "Sales", "Manufacturing Price" e "Date" onde este último referencia a tabela D_Data.

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/2d3c8120-a8d0-453b-b371-cfe455a6819c)


Passo 02 – Referenciando as chaves
Como último passo, é hora de dar forma ao Star Schema. Nesta etapa, faz-se a ligação de todas as chaves referenciais das tabelas dimensões com a tabela fato (sem ligações entre as dimensões. Estamos tratando de um Star Schema e não de um Snowflake Schema).

Segue abaixo o resultado final:

![image](https://github.com/alessandragalvaos/DAX-Power-BI/assets/156546129/42836bcd-71b6-49ca-8aca-78153b9aaa32)



