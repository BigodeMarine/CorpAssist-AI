# Engenharia de Prompts — CorpAssist AI

## 1. Objetivo

A engenharia de prompts é uma parte fundamental do CorpAssist AI. As instruções fornecidas ao agente determinam como ele interpreta as solicitações, organiza as informações e produz os textos corporativos.

O objetivo é garantir que as respostas sejam coerentes com o contexto informado, respeitem a finalidade da comunicação e evitem a criação de informações não fornecidas pelo usuário.

## 2. Configuração do modelo

O agente utiliza:

- Plataforma: Make AI Agent.
- Provedor: Make AI Provider.
- Modelo: Claude Haiku 4.5.
- Entrada: dados estruturados provenientes do Google Sheets.
- Saída: conteúdo textual encaminhado ao Google Docs.

O campo Input recebe os dados da solicitação, enquanto o campo Instructions contém as regras permanentes de comportamento do agente.

Essa separação permite distinguir as informações específicas de cada solicitação das diretrizes gerais que orientam o processamento.

## 3. Estrutura do prompt de entrada

A entrada encaminhada ao agente segue uma estrutura padronizada:

```text
Crie uma comunicação corporativa utilizando os dados abaixo,
recebidos por meio do formulário CorpAssist AI.

Tipo de comunicação: {{1.`1`}}
Objetivo: {{1.`2`}}
Público-alvo: {{1.`3`}}
Canal: {{1.`4`}}
Tom desejado: {{1.`5`}}
Informações principais: {{1.`6`}}
Observações adicionais: {{1.`7`}}

Considere todos os campos preenchidos e siga rigorosamente
as Instructions do agente.
```

Os campos entre chaves são mapeamentos dinâmicos do Make, preenchidos com os dados recebidos da planilha.

Dessa forma, o mesmo agente pode processar diferentes solicitações sem precisar de um prompt completamente novo para cada tipo de comunicação.

## 4. Diretrizes principais das Instructions

As Instructions foram organizadas em blocos temáticos para facilitar a manutenção e o aprimoramento do comportamento do agente.

### Identidade e responsabilidades

Define o papel do CorpAssist AI como assistente de comunicação corporativa e estabelece os tipos de conteúdo que ele pode elaborar ou revisar.

### Fidelidade às informações

Estabelece que o agente não deve inventar nomes, datas, cargos, valores, decisões ou acontecimentos.

Também determina que fatos, decisões e sugestões sejam apresentados de maneira distinta.

### Tratamento de informações ambíguas

Orienta o agente a identificar expressões contraditórias, ofensivas ou com múltiplas interpretações.

Quando uma interpretação puder alterar significativamente o sentido da comunicação, o agente deve sinalizar a questão e solicitar confirmação.

### Regras específicas para revisão de texto

Determina que o formato e a finalidade do conteúdo original sejam preservados.

O agente não deve transformar automaticamente uma revisão em e-mail ou comunicado, nem acrescentar saudações e assinaturas sem solicitação explícita.

### Validação de contexto e público-alvo

Impede que o agente presuma acontecimentos ou situações não apresentados no conteúdo.

Também orienta a sinalização de critérios de segmentação potencialmente discriminatórios ou sem relação clara com a finalidade da comunicação.

### Controle de inferências e registros formais

Estabelece regras para evitar a dedução de datas e a criação de acontecimentos, deliberações ou encerramentos não informados em atas e registros formais.

### Formato da resposta

Define uma estrutura padronizada em texto simples:

```text
Tipo de comunicação: [tipo identificado]

Assunto ou título: [quando aplicável]

Conteúdo:
[Comunicação elaborada]

Observações para revisão:
[Informações que precisam ser conferidas ou complementadas]
```

A saída não deve utilizar formatação Markdown, blocos de código ou caracteres de escape desnecessários.

## 5. Estratégia de validação

O desenvolvimento das instruções foi acompanhado por testes integrados utilizando solicitações reais de demonstração.

Os testes foram utilizados para identificar comportamentos inadequados e aprimorar as regras do agente.

| Teste | Cenário avaliado | Resultado observado |
|---|---|---|
| 1 | Resumo de reunião | Organizou decisões e sinalizou informações ausentes. |
| 2 | Revisão de texto sobre LGPD | Resumiu os tópicos selecionados e identificou pontos que exigiam conferência. |
| 3 | E-mail corporativo | Elaborou uma comunicação profissional sem inventar a data de início. |
| 4 | Comunicado interno | Identificou uma possibilidade de manutenção ainda não confirmada, mas inicialmente inferiu datas que não haviam sido informadas. |
| 5 | Ata de reunião | Separou decisões, encaminhamentos e pendências, mas inicialmente criou uma frase de encerramento não informada. |
| 6 | Mensagem corporativa | Gerou texto simples, preservou as condições informadas e não inventou o prazo mínimo. |
| 7 | Revisão com contradições | Identificou regras conflitantes sem escolher uma interpretação por conta própria. |

## 6. Aprimoramentos realizados

Os testes permitiram identificar pontos que precisavam ser corrigidos nas instruções.

Entre os principais aprimoramentos estão:

- Proibição de deduzir datas a partir de expressões relativas.
- Proibição de inventar encerramentos em atas e registros formais.
- Preservação do formato original durante revisões de texto.
- Identificação explícita de contradições e ambiguidades.
- Diferenciação entre decisões confirmadas e sugestões.
- Padronização da saída em texto simples.
- Utilização de marcadores editáveis para informações ausentes.

Esses ajustes foram realizados diretamente nas Instructions do agente no Make AI Agent.

## 7. Limitações identificadas

Mesmo com instruções específicas, o modelo pode apresentar interpretações incorretas ou observações desnecessárias.

Os testes demonstraram que:

- Algumas instruções podem não ser seguidas perfeitamente em todas as situações.
- O agente pode produzir observações redundantes.
- A interpretação de textos ambíguos depende da clareza das informações recebidas.
- A validação humana continua necessária para confirmar a precisão e a adequação do conteúdo.

## 8. Considerações finais

A construção do prompt foi um processo iterativo, baseado na definição de regras, execução de testes e correção dos comportamentos identificados.

A estratégia adotada demonstra que a qualidade de um agente de IA não depende apenas do modelo utilizado, mas também da clareza das instruções, da estrutura dos dados recebidos e da validação dos resultados.