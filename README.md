# Entrega 1 — Modelo Conceitual (DER)

**Modelagem de um sistema de gestão de informações para o WK Materiais de Construção**

---

## Metadados

**Nomes dos alunos e RGM:** 

`Matheus Pedrosa dos Reis 46784721`

`Pablo Orlando Bizari Di Sisto 46695737`

`Vithor Hugo Moreno de Carvalho 46761926`

---

## Sumário

1. [Caracterização da Organização](#1-caracterização-da-organização)
2. [Processos de Negócio](#2-processos-de-negócio)
3. [Requisitos do Sistema](#3-requisitos-do-sistema)
4. [Regras de Negócio](#4-regras-de-negócio)
5. [Dicionário de Dados Conceitual](#5-dicionário-de-dados-conceitual)
6. [Modelagem Conceitual (Entidades e Relacionamentos)](#6-modelagem-conceitual-entidades-e-relacionamentos)
7. [Diagrama Entidade-Relacionamento (DER)](#7-diagrama-entidade-relacionamento-der)
8. [Justificativa Técnica](#8-justificativa-técnica)
9. [Uso de Inteligência Artificial](#9-uso-de-inteligência-artificial)

---

## 1. Caracterização da Organização

### Nome e natureza da organização

| Campo             | Informação                                                                                   |
| ----------------- | -------------------------------------------------------------------------------------------- |
| **Nome fantasia** | WK Materiais de Construção                                                                   |
| **Razão social**  | David Caravanti de Oliveira                                                                  |
| **CNPJ**          | 30.112.168/0001-50                                                                           |
| **Natureza**      | Empresa comercial privada de pequeno porte (varejo de materiais de construção e ferramentas) |

### Contexto e porte

- A empresa atua há **18 anos e 6 meses** no mesmo endereço.
- A equipe operacional é enxuta, com **4 pessoas**: o proprietário Wanderley, 2 balconistas e 1 estoquista.
- Volume médio de atendimento: **25 vendas por dia**, com faturamento diário médio de **R$ 1.200,00**.
- A loja é especializada em miudezas de construção e ferramentas de fácil locomoção.
- Atua **exclusivamente na modalidade de retirada no local** (não realiza entregas).

### Problemas e necessidades identificados

O depósito opera de forma **100% manual ("no papel")**, e o processo de orçamento e consulta de estoque é verbal ("boca a boca"). Isso gera ausência de controle sobre:

- fluxo de caixa;
- histórico de vendas;
- estoque;
- saldo devedor das vendas a prazo ("fiado").

Embora não haja contabilização exata de perdas, a informalidade gera alto risco operacional e de liquidez.

### Justificativa da escolha

Trata-se de uma organização real, com acesso direto garantido ao proprietário para levantamento de requisitos. O foco operacional sem logística externa permite um detalhamento profundo das rotinas de vendas presenciais, controle de estoque, compras e contas a receber.

### Evidências da organização

- **Endereço:** Rua Conêgo Antônio Dias Pequeno, nº 552
- **Contato:** Wanderley (Proprietário)

> 📎 *[Anexado fotos do pátio/loja e link do Google Maps/Google Meu Negócio]*

---

## 2. Processos de Negócio

### Principais processos mapeados

1. **Atendimento e Orçamento de Balcão**
   Consulta verbal de preços e verificação presencial do estoque pelo balconista/estoquista.

2. **Venda e Recebimento no Balcão**
   Registro manual do pedido.
   
   - Pagamentos aceitos: Cartão (Débito/Crédito), PIX ou Dinheiro.
   - Vendas à vista (Dinheiro ou PIX) possuem **desconto automático de 5%**.
   - A mercadoria é entregue diretamente ao cliente na loja.

3. **Venda a Prazo ("Fiado")**
   Modalidade baseada em relação de confiança. Anotação manual dos débitos, sem cadastro formal ou limite pré-definido de crédito.

4. **Trocas e Devoluções**
   Recebimento de sobras de obra ou mercadorias com defeito. O depósito gera crédito interno para nova compra ou realiza a troca direta por itens de mesmo valor.

5. **Gestão de Compras e Reposição**
   Compras sob demanda (sem data fixa), baseadas no menor preço entre múltiplos fornecedores. Cada ordem de compra exige valor mínimo de **R$ 1.500,00 por fornecedor**.

---

## 3. Requisitos do Sistema

### 3.1 Requisitos Funcionais

| ID       | Requisito                                 | Descrição                                                                                                           |
| -------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **RF01** | Cadastrar e Consultar Produtos            | Permitir o registro e a busca de materiais com código, descrição, categoria, preço e quantidade em estoque.         |
| **RF02** | Cadastrar Clientes                        | Permitir o cadastro de clientes (obrigatório para vendas a prazo/fiado e opcional para vendas presenciais à vista). |
| **RF03** | Registrar Venda                           | Registrar a venda no balcão indicando itens, quantidades, forma de pagamento e cliente (quando aplicável).          |
| **RF04** | Conceder Desconto Automático              | Aplicar desconto de 5% sobre o valor total da venda quando a forma de pagamento for Dinheiro ou PIX.                |
| **RF05** | Gerenciar Contas a Receber (Fiado)        | Registrar o saldo devedor de vendas a prazo vinculado ao cliente e permitir a baixa após quitação.                  |
| **RF06** | Registrar Trocas e Devoluções             | Registrar a devolução de produtos, reajustando o estoque e gerando crédito vinculado ao cliente.                    |
| **RF07** | Cadastrar Fornecedores e Ordens de Compra | Cadastrar fornecedores e registrar os pedidos de compra de mercadorias.                                             |
| **RF08** | Validar Valor Mínimo de Compra            | Impedir o fechamento de ordem de compra com valor total inferior a R$ 1.500,00 por fornecedor.                      |
| **RF09** | Baixa e Entrada de Estoque                | Atualizar automaticamente o saldo de estoque ao concluir vendas (baixa) ou receber compras/devoluções (entrada).    |

### 3.2 Requisitos Não Funcionais

| ID        | Requisito   | Descrição                                                                                                     |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------- |
| **RNF01** | Usabilidade | Interface simples para registro ágil de vendas no balcão, sem gerar filas.                                    |
| **RNF02** | Desempenho  | Abertura e fechamento de vendas efetuados em tempo inferior a 2 segundos.                                     |
| **RNF03** | Integridade | Nenhuma movimentação física de estoque pode ocorrer sem vínculo com uma Venda, Devolução ou Pedido de Compra. |

---

## 4. Regras de Negócio

### Regras operacionais

| ID       | Regra                                   | Descrição                                                                                         |
| -------- | --------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **RO01** | Desconto à Vista                        | Desconto fixo de 5% para pagamentos em Dinheiro ou PIX.                                           |
| **RO02** | Exclusividade da Modalidade Retira      | Todas as vendas são concluídas no balcão (sem entregas ou fretes).                                |
| **RO03** | Cadastro Obrigatório para Venda a Prazo | Proibido efetuar venda na modalidade "Fiado" sem vínculo com um CLIENTE cadastrado.               |
| **RO04** | Valor Mínimo de Ordem de Compra         | Ordens de compra para fornecedores exigem valor total igual ou superior a R$ 1.500,00.            |
| **RO05** | Política de Devolução                   | Devoluções não geram devolução em dinheiro, apenas crédito interno ou troca por item equivalente. |

### Restrições organizacionais

- A operação enxuta (poucos funcionários) exige reduzida burocracia na digitação de dados durante o atendimento.

---

## 5. Dicionário de Dados Conceitual

### 5.1 Convenções do Dicionário

- **SGBD:** MySQL 8, mecanismo de armazenamento InnoDB (garante consistência transacional ACID e chaves estrangeiras).
- **Codificação de caracteres:** `utf8mb4` com collation `utf8mb4_0900_ai_ci` (suporta acentuação em português e caracteres especiais).

#### Notação formal

| Símbolo      | Significado                                 |
| ------------ | ------------------------------------------- |
| `=`          | é composto de                               |
| `+`          | e (conecta elementos obrigatórios)          |
| `()`         | opcional                                    |
| `{}`, `n{}m` | iteração com limite mínimo *n* e máximo *m* |
| `[]`         | escolha obrigatória entre alternativas      |
| `//`         | rótulo de um grupo repetitivo               |
| `@`          | identificador (chave primária)              |
| `**`         | comentário                                  |

#### Prefixos padronizados

| Prefixo | Significado                                |
| ------- | ------------------------------------------ |
| `ID_`   | Identificador (chave primária/estrangeira) |
| `NM_`   | Nome / Razão Social                        |
| `DT_`   | Data / Data e hora                         |
| `TP_`   | Tipo / Categoria de domínio                |
| `VL_`   | Valor monetário                            |
| `QT_`   | Quantidade numérica                        |
| `DS_`   | Descrição livre                            |
| `IN_`   | Indicador booleano (Sim/Não)               |
| `NR_`   | Número de documento / registro             |

---

### 5.2 Estrutura das Entidades

#### Entidade: CLIENTE

```text
CLIENTE = @ID_CLIENTE + NM_CLIENTE + (NR_CPF_CNPJ) + (NR_TELEFONE) + (DS_ENDERECO) + IN_ATIVO
```

**Leitura:** `@ID_CLIENTE` e `NM_CLIENTE` são obrigatórios; documentos e contatos vêm entre `()` por serem opcionais nas compras à vista, mas exigidos nas vendas a prazo. `IN_ATIVO` indica a situação do cadastro.

| Atributo      | Tipo físico  | Obrigatório | Significado e relevância                                           |
| ------------- | ------------ | ----------- | ------------------------------------------------------------------ |
| `ID_CLIENTE`  | integer      | Sim (PK)    | Código identificador único do cliente no sistema.                  |
| `NM_CLIENTE`  | varchar(120) | Sim         | Nome completo ou razão social do cliente.                          |
| `NR_CPF_CNPJ` | varchar(18)  | Não         | CPF ou CNPJ do cliente. Obrigatório para vendas a prazo (RO03).    |
| `NR_TELEFONE` | varchar(20)  | Não         | Número de telefone/WhatsApp para contato e cobrança.               |
| `DS_ENDERECO` | varchar(200) | Não         | Endereço residencial ou comercial do cliente.                      |
| `IN_ATIVO`    | boolean      | Sim         | Indicador de cadastro ativo (TRUE para ativo, FALSE para inativo). |

**Índices:** PK `ID_CLIENTE`; índice secundário em `NM_CLIENTE` (busca na venda) e `NR_CPF_CNPJ` (busca por documento).

---

#### Entidade: PRODUTO

```text
PRODUTO = @ID_PRODUTO + NM_PRODUTO + (DS_CATEGORIA) + VL_PRECO_VENDA + QT_ESTOQUE + IN_ATIVO
```

**Leitura:** `@ID_PRODUTO`, `NM_PRODUTO`, `VL_PRECO_VENDA` e `QT_ESTOQUE` são obrigatórios. `DS_CATEGORIA` é opcional, para agrupamento do catálogo.

| Atributo         | Tipo físico   | Obrigatório | Significado e relevância                                               |
| ---------------- | ------------- | ----------- | ---------------------------------------------------------------------- |
| `ID_PRODUTO`     | integer       | Sim (PK)    | Código identificador único do produto.                                 |
| `NM_PRODUTO`     | varchar(120)  | Sim         | Descrição comercial da mercadoria (ex.: "Saco de Cimento CP-II 50kg"). |
| `DS_CATEGORIA`   | varchar(60)   | Não         | Categoria do material (ex.: "Alvenaria", "Hidráulica", "Elétrica").    |
| `VL_PRECO_VENDA` | decimal(10,2) | Sim         | Preço unitário de venda cadastrado. Deve ser maior que zero.           |
| `QT_ESTOQUE`     | decimal(10,2) | Sim         | Quantidade física disponível em loja/pátio.                            |
| `IN_ATIVO`       | boolean       | Sim         | Indicador de produto ativo no catálogo.                                |

**Índices:** PK `ID_PRODUTO`; índice em `NM_PRODUTO` (busca rápida no balcão).

---

#### Entidade: VENDA

```text
VENDA = @ID_VENDA + DT_VENDA + [TP_DINHEIRO | TP_PIX | TP_CARTAO | TP_FIADO]
        + VL_TOTAL + VL_DESCONTO + (ID_CLIENTE)
        + 1{/ITEM_VENDA/ = ID_PRODUTO + QT_VENDIDA + VL_UNITARIO_APLICADO}n
```

**Leitura:** A venda exige selecionar exatamente um tipo de pagamento em `[]`. Possui uma iteração de 1 a *n* itens em `{/ITEM_VENDA/}`. `ID_CLIENTE` é opcional para vendas à vista e obrigatório para `TP_FIADO`.

| Atributo                            | Tipo físico   | Obrigatório | Significado e relevância                                       |
| ----------------------------------- | ------------- | ----------- | -------------------------------------------------------------- |
| `ID_VENDA`                          | integer       | Sim (PK)    | Identificador único da transação de venda.                     |
| `DT_VENDA`                          | datetime      | Sim         | Data e hora em que a venda foi realizada.                      |
| `TP_PAGAMENTO`                      | varchar(20)   | Sim         | Forma de pagamento escolhida (DINHEIRO, PIX, CARTAO, FIADO).   |
| `VL_TOTAL`                          | decimal(10,2) | Sim         | Valor final da venda após aplicar o desconto (se houver).      |
| `VL_DESCONTO`                       | decimal(10,2) | Sim         | Valor do desconto aplicado (5% para Dinheiro/PIX via RO01).    |
| `ID_CLIENTE`                        | integer       | Não (FK)    | Vínculo com o cliente (obrigatório se `TP_PAGAMENTO = FIADO`). |
| `ID_PRODUTO` *(por item)*           | integer       | Sim (FK)    | Código do produto vendido.                                     |
| `QT_VENDIDA` *(por item)*           | decimal(10,2) | Sim         | Quantidade vendida do produto.                                 |
| `VL_UNITARIO_APLICADO` *(por item)* | decimal(10,2) | Sim         | Preço unitário praticado na venda (preserva histórico).        |

**Índices:** PK `ID_VENDA`; FK `ID_CLIENTE` (localizar vendas do cliente); índice em `DT_VENDA` (relatórios diários).

---

#### Entidade: CONTAS_A_RECEBER (Fiado)

```text
CONTAS_A_RECEBER = @ID_CONTA + ID_VENDA + ID_CLIENTE + VL_DEBITO + DT_LANCAMENTO + [TP_PENDENTE | TP_PAGO]
```

**Leitura:** Registro financeiro de pendência originado exclusivamente por vendas a prazo (`TP_FIADO`).

| Atributo        | Tipo físico   | Obrigatório     | Significado e relevância                    |
| --------------- | ------------- | --------------- | ------------------------------------------- |
| `ID_CONTA`      | integer       | Sim (PK)        | Identificador da conta a receber.           |
| `ID_VENDA`      | integer       | Sim (FK, Único) | Referência à venda a prazo originária.      |
| `ID_CLIENTE`    | integer       | Sim (FK)        | Vínculo obrigatório com o cliente devedor.  |
| `VL_DEBITO`     | decimal(10,2) | Sim             | Valor total pendente de quitação.           |
| `DT_LANCAMENTO` | date          | Sim             | Data do registro da dívida.                 |
| `TP_STATUS`     | varchar(15)   | Sim             | Situação atual da conta (PENDENTE ou PAGO). |

**Índices:** PK `ID_CONTA`; FK `ID_VENDA`; FK `ID_CLIENTE` (extrato de dívidas por cliente).

---

#### Entidade: FORNECEDOR

```text
FORNECEDOR = @ID_FORNECEDOR + NM_RAZAO_SOCIAL + NR_CNPJ + NR_TELEFONE + IN_ATIVO
```

**Leitura:** Todos os campos cadastrais do fornecedor de materiais são obrigatórios.

| Atributo          | Tipo físico  | Obrigatório | Significado e relevância                              |
| ----------------- | ------------ | ----------- | ----------------------------------------------------- |
| `ID_FORNECEDOR`   | integer      | Sim (PK)    | Identificador do fornecedor.                          |
| `NM_RAZAO_SOCIAL` | varchar(120) | Sim         | Razão Social ou Nome Fantasia da empresa fornecedora. |
| `NR_CNPJ`         | varchar(18)  | Sim (Único) | CNPJ do fornecedor.                                   |
| `NR_TELEFONE`     | varchar(20)  | Sim         | Telefone de contato para cotações e compras.          |
| `IN_ATIVO`        | boolean      | Sim         | Status do fornecedor no sistema.                      |

**Índices:** PK `ID_FORNECEDOR`; índice único em `NR_CNPJ`.

---

#### Entidade: PEDIDO_COMPRA

```text
PEDIDO_COMPRA = @ID_PEDIDO_COMPRA + ID_FORNECEDOR + DT_PEDIDO + VL_TOTAL_PEDIDO
                + [TP_PENDENTE | TP_RECEBIDO]
                + 1{/ITEM_COMPRA/ = ID_PRODUTO + QT_COMPRADA + VL_CUSTO_UNITARIO}n
```

**Leitura:** Ordem de compra enviada ao fornecedor. O somatório de `VL_TOTAL_PEDIDO` deve ser **≥ R$ 1.500,00** (RO04).

| Atributo                         | Tipo físico   | Obrigatório | Significado e relevância                                    |
| -------------------------------- | ------------- | ----------- | ----------------------------------------------------------- |
| `ID_PEDIDO_COMPRA`               | integer       | Sim (PK)    | Código identificador da ordem de compra.                    |
| `ID_FORNECEDOR`                  | integer       | Sim (FK)    | Fornecedor escolhido para a compra.                         |
| `DT_PEDIDO`                      | date          | Sim         | Data de emissão da ordem de compra.                         |
| `VL_TOTAL_PEDIDO`                | decimal(10,2) | Sim         | Valor total do pedido (deve atender à RO04: ≥ R$ 1.500,00). |
| `TP_STATUS`                      | varchar(15)   | Sim         | Situação do pedido (PENDENTE ou RECEBIDO).                  |
| `ID_PRODUTO` *(por item)*        | integer       | Sim (FK)    | Produto a ser reposto.                                      |
| `QT_COMPRADA` *(por item)*       | decimal(10,2) | Sim         | Quantidade encomendada.                                     |
| `VL_CUSTO_UNITARIO` *(por item)* | decimal(10,2) | Sim         | Preço de custo negociado por unidade.                       |

**Índices:** PK `ID_PEDIDO_COMPRA`; FK `ID_FORNECEDOR`.

---

### 5.3 Log de Acesso (Metadado Operacional)

A matriz abaixo define as permissões operacionais de gravação e consulta no SGBD por papel operacional no depósito:

| Tabela               | LER (Select)                         | INSERIR (Insert)          | ATUALIZAR (Update)                    | APAGAR (Delete)                           |
| -------------------- | ------------------------------------ | ------------------------- | ------------------------------------- | ----------------------------------------- |
| **CLIENTE**          | Proprietário, Balconista             | Proprietário, Balconista  | Proprietário, Balconista              | Nenhum (apenas inativação via `IN_ATIVO`) |
| **PRODUTO**          | Proprietário, Balconista, Estoquista | Proprietário              | Proprietário, Estoquista (estoque)    | Nenhum (inativação via `IN_ATIVO`)        |
| **VENDA**            | Proprietário, Balconista             | Balconista                | Nenhum (venda fechada não se edita)   | Nenhum                                    |
| **CONTAS_A_RECEBER** | Proprietário, Balconista             | Sistema (via Venda Fiado) | Proprietário (baixa de pagamento)     | Nenhum                                    |
| **FORNECEDOR**       | Proprietário                         | Proprietário              | Proprietário                          | Proprietário                              |
| **PEDIDO_COMPRA**    | Proprietário, Estoquista             | Proprietário              | Proprietário (confirmação de entrega) | Proprietário                              |

---

### 5.4 Conformidade com a LGPD e Privacidade

- **Tratamento de dados de clientes:** a tabela `CLIENTE` coleta dados pessoais comuns (Nome, CPF, Telefone, Endereço). O tratamento fundamenta-se na execução de contrato / relação de crédito (**Art. 7º, V da LGPD**) para vendas na modalidade "Fiado".
- **Minimização de dados:** para vendas presenciais à vista (Dinheiro, PIX ou Cartão), o cadastro de cliente é totalmente opcional, garantindo a preservação da privacidade.
- **Exemplos fictícios:** todos os dados ilustrativos no dicionário e nos testes são fictícios, preservando o sigilo dos clientes reais do depósito.

---

## 6. Modelagem Conceitual (Entidades e Relacionamentos)

### Entidades reconhecidas

`CLIENTE`, `PRODUTO`, `VENDA`, `ITEM_VENDA` *(associativa)*, `CONTAS_A_RECEBER`, `FORNECEDOR`, `PEDIDO_COMPRA`, `ITEM_PEDIDO_COMPRA` *(associativa)*.

### Mapeamento de cardinalidades

| Relacionamento                     | Cardinalidade  | Observação                                                         |
| ---------------------------------- | -------------- | ------------------------------------------------------------------ |
| CLIENTE — VENDA                    | (1,1) ── (0,N) | Cliente pode ter várias vendas; venda à vista pode ter 0 clientes. |
| VENDA — ITEM_VENDA                 | (1,1) ── (1,N) | Toda venda possui ao menos um item.                                |
| ITEM_VENDA — PRODUTO               | (N,1) ── (1,1) | Cada item refere-se a um único produto.                            |
| VENDA — CONTAS_A_RECEBER           | (1,1) ── (0,1) | Gera conta apenas se pagamento = FIADO.                            |
| CONTAS_A_RECEBER — CLIENTE         | (N,1) ── (1,1) | Cada conta pertence a um cliente devedor.                          |
| FORNECEDOR — PEDIDO_COMPRA         | (1,1) ── (0,N) | Fornecedor pode ter vários pedidos.                                |
| PEDIDO_COMPRA — ITEM_PEDIDO_COMPRA | (1,1) ── (1,N) | Todo pedido possui ao menos um item.                               |
| ITEM_PEDIDO_COMPRA — PRODUTO       | (N,1) ── (1,1) | Cada item refere-se a um único produto.                            |

---

## 7. Diagrama Entidade-Relacionamento (DER)

> 🖼️ *A imagem do diagrama DER está anexada à pasta do repositório no GitHub.*

<!-- Exemplo: ![DER - WK Materiais de Construção](./der.png) -->

---

## 8. Justificativa Técnica

- **Omissão de módulos de frota/frete:** entidades como Veículo, Motorista ou Frete foram intencionalmente excluídas do modelo conceitual, pois a pesquisa comprovou que a empresa atua estritamente na modalidade "Retira".
- **Cardinalidade opcional do Cliente na Venda:** permite registrar vendas rápidas à vista sem exigência de cadastro, evitando gargalos no atendimento presencial de balcão.
- **Entidades associativas para histórico de preços:** `ITEM_VENDA` e `ITEM_PEDIDO_COMPRA` registram os preços negociados na data da transação (`VL_UNITARIO_APLICADO` e `VL_CUSTO_UNITARIO`), impedindo que alterações futuras no catálogo distorçam o histórico financeiro.

---

## 9. Uso de Inteligência Artificial

### Google Gemini 3.1 Pro

| Item                   | Registro de uso                                                                                                                              |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ferramenta e etapa** | Google Gemini 3.1 Pro — organização da entrevista com o proprietário e estruturação inicial do README no padrão formal da Entrega 1.        |
| **Motivação**          | Formatar os dados brutos colhidos na visita de campo segundo a notação técnica formal exigida (seções, títulos, tabelas e requisitos).      |
| **Prompt utilizado**   | *"Refaça o esqueleto se baseando no novo modelo do dicionário de dados formal, mantendo todos os processos e regras de negócio levantados."* |
| **Verificação**        | Comparação da versão sugerida com o esqueleto oficial da entrega e com as anotações da entrevista com Wanderley, ajustando termos e nomes.  |
| **Ajustes manuais**    | Remoção de campos e entidades de entrega/frete sugeridos automaticamente pela IA e correção de trechos que não refletiam o caso real WK.     |


### ChatGPT gratuito

| Item                   | Registro de uso                                                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ferramenta e etapa** | ChatGPT (versão gratuita) — geração da imagem do Diagrama Entidade-Relacionamento (DER) a partir da lista de entidades e relacionamentos.   |
| **Motivação**          | Produzir rapidamente um DER visual no estilo visto em aula, facilitando a validação de cardinalidades e chaves antes de finalizar a entrega. |
| **Prompt utilizado**   | *"Com base nas entidades CLIENTE, PRODUTO, VENDA, CONTAS_A_RECEBER, FORNECEDOR, PEDIDO_COMPRA e ITENS, monte um DER com cardinalidades."*    |
| **Verificação**        | Checagem manual das cardinalidades e das chaves sugeridas pela IA em relação ao dicionário de dados e às regras operacionais descritas.     |
| **Ajustes manuais**    | Correção de nomes de entidades, remoção de relacionamentos não previstos nos requisitos e pequenos ajustes de layout antes de salvar a imagem.|


### Perplexity Pro Vivo

| Item                   | Registro de uso                                                                                                                                                 |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ferramenta e etapa** | Perplexity Pro Vivo — apoio na construção e refinamento do dicionário de dados conceitual em HTML, alinhando a estrutura com o exemplo de prontuário e o README. |
| **Motivação**          | Garantir que o dicionário de dados tivesse metadados completos (tipo, obrigatoriedade, significado) e coerência com o DER, regras de negócio e fluxo descritos.  |
| **Prompt utilizado**   | *"Tenho a entrega de um trabalho: converta o dicionário de dados do WK para HTML seguindo o modelo do professor, humanize o texto e mantenha todas as regras."*   |
| **Verificação**        | Revisão de cada tabela gerada comparando com o DER profissional, requisitos funcionais e anotações de campo, ajustando descrições que não refletiam o funcionamento real. |
| **Ajustes manuais**    | Humanização da linguagem (remoção de trechos com ‘cara de IA’), inclusão/remoção de atributos conforme o modelo conceitual e ajustes finos para seguir o exemplo dado. |