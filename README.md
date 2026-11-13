# CorpAssist AI — Assistente Inteligente de Comunicação Corporativa

## 1. Sobre o projeto

O CorpAssist AI é um assistente inteligente de comunicação corporativa desenvolvido como parte do projeto acadêmico "Seu Primeiro Agente de IA: Criando um Assistente Corporativo Inteligente com IA Generativa e Automação".

A solução utiliza Inteligência Artificial Generativa para auxiliar na criação, organização, resumo e revisão de textos corporativos.

O objetivo é reduzir o tempo necessário para elaborar comunicações profissionais, mantendo clareza, coerência e adequação ao público-alvo, ao canal e à finalidade da mensagem.

O assistente recebe informações estruturadas, interpreta o contexto utilizando um modelo de linguagem (LLM) e gera um rascunho para revisão humana.

**Importante:** o sistema não envia nem publica comunicações automaticamente. Todo conteúdo gerado deve ser revisado e aprovado por uma pessoa antes de sua utilização.

## 2. Funcionalidades

O CorpAssist AI permite solicitar:

- E-mails corporativos;
- Comunicados internos;
- Resumos de reunião;
- Atas de reunião;
- Mensagens corporativas;
- Revisões de texto.

O conteúdo é elaborado considerando:

- Tipo e objetivo da comunicação;
- Público-alvo;
- Canal de comunicação;
- Tom desejado;
- Informações principais;
- Observações adicionais.

O agente também possui instruções para identificar ambiguidades, contradições e informações ausentes, evitando assumir dados que não foram fornecidos pelo usuário.

## 3. Tecnologias e ferramentas

| Ferramenta | Finalidade |
|---|---|
| Google Forms | Coleta estruturada das solicitações. |
| Google Sheets | Armazenamento das respostas do formulário. |
| Make | Integração das ferramentas e execução da automação. |
| Make AI Agent | Interpretação das solicitações e geração dos textos. |
| Claude Haiku 4.5 | Modelo de linguagem utilizado pelo agente. |
| Google Docs | Armazenamento dos documentos gerados. |

## 4. Arquitetura e fluxo de funcionamento

O funcionamento da solução ocorre nas seguintes etapas:

1. O usuário preenche o formulário Google Forms com os dados da comunicação desejada.
2. As respostas são registradas automaticamente no Google Sheets.
3. O Make monitora a planilha por meio do módulo Google Sheets — Watch New Rows.
4. Quando uma nova resposta é identificada, os dados são encaminhados ao Make AI Agent.
5. O agente interpreta as informações utilizando o modelo Claude Haiku 4.5 e as instruções configuradas.
6. O conteúdo gerado é encaminhado ao Google Docs.
7. O usuário consulta o documento, revisa as informações e aprova sua utilização.

### Representação do fluxo

Google Forms → Google Sheets → Make (Watch New Rows) → Make AI Agent (Claude Haiku 4.5) → Google Docs → Revisão humana.

O cenário do Make está configurado para verificar novas respostas automaticamente a cada 15 minutos.

## 5. Prompt e instruções do agente

O agente foi configurado para atuar como um assistente de comunicação corporativa, seguindo diretrizes específicas.

### Identidade e finalidade

- Elaborar e-mails, comunicados, atas, resumos e mensagens corporativas.
- Revisar e organizar textos existentes.
- Adaptar a comunicação ao público, canal, objetivo e tom informados.

### Fidelidade às informações

- Não inventar nomes, datas, cargos, departamentos, valores ou decisões.
- Preservar o significado das informações recebidas.
- Diferenciar fatos, decisões e sugestões.
- Utilizar marcadores editáveis quando informações necessárias estiverem ausentes.

### Tratamento de ambiguidades

- Identificar informações contraditórias ou com mais de uma interpretação.
- Não escolher uma interpretação por conta própria.
- Sinalizar inconsistências e solicitar confirmação quando necessário.

### Revisão de texto

- Preservar o formato e a finalidade do conteúdo original.
- Não transformar automaticamente uma revisão em e-mail ou comunicado.
- Destacar informações importantes sem distorcer o significado.

### Registros formais

- Não inventar participantes, acontecimentos, decisões ou encerramentos de reuniões.
- Não deduzir datas completas a partir de referências temporais relativas.
- Sinalizar informações incompletas em atas e documentos formais.

### Segurança e supervisão humana

- Gerar somente rascunhos.
- Não enviar ou publicar comunicações automaticamente.
- Evitar solicitar dados pessoais desnecessários.
- Manter a revisão e a aprovação humana como etapas obrigatórias.

## 6. Como utilizar

1. Acesse o formulário de solicitação do CorpAssist AI.
2. Selecione o tipo de comunicação desejado.
3. Informe o objetivo e o público-alvo.
4. Escolha o canal e o tom da comunicação.
5. Preencha as informações principais.
6. Acrescente observações adicionais, se necessário.
7. Envie o formulário.
8. Aguarde o processamento automático pelo cenário do Make.
9. Consulte o documento gerado no Google Docs.
10. Revise o conteúdo e confirme se as informações estão corretas antes de utilizá-lo.

## 7. Testes e validação

Foram realizados testes integrados para avaliar a coerência, a fidelidade às informações e o comportamento do agente em diferentes situações.

Os cenários testados incluíram:

- Resumo de reunião com decisões e informações incompletas.
- Revisão de texto sobre orientações relacionadas à LGPD.
- Elaboração de e-mail sobre alteração do horário de expediente.
- Comunicado interno sobre manutenção programada.
- Ata de reunião com decisões e pendências.
- Mensagem corporativa sobre solicitação de férias.
- Revisão de texto com contradições entre regras de trabalho presencial, remoto e híbrido.

Os testes demonstraram que o agente consegue adaptar a estrutura da resposta ao tipo de comunicação, preservar as informações fornecidas e sinalizar ambiguidades, contradições e dados ausentes.

Durante a validação, as instruções foram aprimoradas para reduzir inferências indevidas, evitar informações inventadas e padronizar a formatação dos documentos.

## 8. Evidências

As evidências da implementação e dos testes serão organizadas no diretório `evidencias/`.

- `evidencias/formulario.png` — formulário de entrada.
- `evidencias/google-sheets.png` — planilha de respostas.
- `evidencias/workflow-make.png` — cenário de automação.
- `evidencias/agente-ia.png` — configuração do agente e modelo.
- `evidencias/teste-email.png` — exemplo de e-mail gerado.
- `evidencias/teste-ata.png` — exemplo de ata gerada.
- `evidencias/teste-revisao.png` — exemplo de revisão com contradições.
- `evidencias/teste-mensagem.png` — exemplo de mensagem corporativa.

## 9. Acesso à solução

- **Formulário:** [[GOOGLE FORMS](https://docs.google.com/forms/d/e/1FAIpQLSdu9EVH7Z1Sx-o7nx-tF0rHF-ya2ZEbjdAKQ1VoU0JujU2GNw/viewform)]
- **Cenário do Make:** [[MAKE SCENARIO](https://us2.make.com/public/shared-scenario/PztKdkIu2k5/corp-assist-ai-automacao-de-comunicacao)]
- **Documentos de demonstração:** [[DOCS DOS TESTES](https://drive.google.com/drive/folders/1vPHdQ16UewZF47ocFDyLsQVfYzp4yLGk?usp=drive_link)]

## 10. Limitações e supervisão humana

A utilização de Inteligência Artificial Generativa apresenta limitações. O modelo pode interpretar informações incorretamente, produzir conteúdo inadequado ou deixar de identificar alguma inconsistência.

Por esse motivo, o conteúdo gerado não deve ser considerado uma comunicação oficialmente aprovada.

A revisão humana é indispensável, especialmente em comunicações que envolvam informações confidenciais, dados pessoais, decisões organizacionais ou orientações jurídicas.

O CorpAssist AI utiliza a inteligência artificial como ferramenta de apoio à produtividade, mantendo a responsabilidade pela comunicação final com o usuário.
