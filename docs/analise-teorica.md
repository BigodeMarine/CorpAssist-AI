# Análise Teórica — CorpAssist AI

## 1. Contextualização do problema

A comunicação corporativa exige clareza, organização e adequação da linguagem ao público e à finalidade de cada mensagem.

No ambiente profissional, a elaboração de e-mails, comunicados, atas, resumos e mensagens internas pode consumir tempo dos colaboradores. Além disso, informações incompletas, ambiguidades e contradições podem comprometer a compreensão das comunicações.

Diante desse cenário, foi desenvolvido o CorpAssist AI, um assistente inteligente que utiliza Inteligência Artificial Generativa e automação para auxiliar na elaboração e revisão de textos corporativos.

A solução recebe informações estruturadas do usuário, interpreta o contexto e gera conteúdos adequados ao objetivo, público, canal e tom desejado.

O sistema foi projetado para atuar como ferramenta de apoio à produtividade, mantendo a revisão e a aprovação humana como etapas obrigatórias.

## 2. Modelo de Inteligência Artificial utilizado

O CorpAssist AI utiliza o modelo Claude Haiku 4.5, da Anthropic, integrado por meio do Make AI Provider e utilizado no módulo Make AI Agent.

A escolha foi realizada considerando a disponibilidade do modelo na plataforma, sua adequação a tarefas de interpretação e geração de textos e a proposta de desenvolver uma solução automatizada para solicitações corporativas.

O modelo é utilizado para:

- Interpretar as informações recebidas pelo formulário.
- Identificar o tipo e a finalidade da comunicação.
- Adequar a linguagem ao público e ao canal.
- Organizar e resumir informações.
- Identificar ambiguidades e contradições.
- Gerar rascunhos estruturados para revisão.

A escolha representa uma decisão prática de implementação. Não foi realizado um benchmark comparativo entre diferentes modelos, portanto não se afirma que o Claude Haiku 4.5 seja superior às demais alternativas.

## 3. Estratégia de prompts e instruções

A estratégia de engenharia de prompts foi desenvolvida para orientar o comportamento do agente e reduzir respostas inadequadas.

A solução utiliza duas camadas principais:

### Entrada dinâmica

O formulário coleta informações específicas de cada solicitação:

- Tipo de comunicação;
- Objetivo;
- Público-alvo;
- Canal;
- Tom desejado;
- Informações principais;
- Observações adicionais.

Esses dados são encaminhados dinamicamente pelo Make ao campo Input do agente.

### Instruções permanentes

O campo Instructions define as regras gerais de comportamento do agente.

Entre as principais diretrizes estão:

- Não inventar informações, nomes, datas ou decisões.
- Preservar o significado do conteúdo original.
- Identificar informações ambíguas ou contraditórias.
- Não transformar automaticamente uma revisão em outro tipo de comunicação.
- Não deduzir datas ou acontecimentos ausentes.
- Utilizar marcadores editáveis quando necessário.
- Sinalizar informações que precisam de confirmação.
- Gerar respostas em texto simples e estruturado.
- Não enviar ou publicar comunicações automaticamente.

As instruções foram aprimoradas progressivamente a partir dos resultados dos testes integrados.

## 4. Fluxo de funcionamento da solução

O CorpAssist AI utiliza ferramentas integradas por meio do Make.

O processamento ocorre da seguinte forma:

1. O usuário preenche o formulário Google Forms.
2. As respostas são armazenadas no Google Sheets.
3. O Make monitora a planilha por meio do módulo Watch New Rows.
4. Os dados da nova solicitação são encaminhados ao Make AI Agent.
5. O agente interpreta os dados utilizando as Instructions configuradas.
6. O Claude Haiku 4.5 processa a solicitação e gera o conteúdo.
7. O resultado é encaminhado ao Google Docs.
8. O usuário revisa e aprova o documento antes de utilizá-lo.

O cenário está configurado para verificar novas respostas a cada 15 minutos.

Essa arquitetura demonstra a integração entre entrada estruturada, processamento por LLM, agente de IA e automação de documentos, indo além de uma interação isolada com um chatbot.

## 5. Benefícios da solução

Entre os principais benefícios identificados estão:

- Redução do esforço necessário para elaborar comunicações corporativas.
- Padronização da estrutura dos textos.
- Adaptação da linguagem conforme o público e o canal.
- Organização de informações recebidas de maneira não estruturada.
- Identificação de ambiguidades e contradições.
- Apoio à revisão e ao resumo de conteúdos.
- Automatização de etapas operacionais por meio do Make.

Outro benefício importante é a possibilidade de utilizar o mesmo agente para diferentes tipos de comunicação, sem precisar construir um fluxo independente para cada solicitação.

## 6. Limitações e necessidade de supervisão humana

A Inteligência Artificial Generativa pode produzir informações incorretas, interpretar inadequadamente uma solicitação ou deixar de identificar alguma inconsistência.

Durante os testes do CorpAssist AI, foram identificados comportamentos que exigiram aprimoramentos nas instruções, como:

- Inferência de datas que não haviam sido informadas.
- Inclusão de frases de encerramento não presentes nas informações originais.
- Transformação de uma revisão de texto em formato de e-mail.
- Produção de observações redundantes.

Esses resultados demonstram que instruções bem definidas ajudam a orientar o modelo, mas não garantem que todos os resultados sejam perfeitos.

Por isso, a supervisão humana é necessária para:

- Conferir datas, nomes, valores e informações relevantes.
- Validar decisões e encaminhamentos registrados.
- Avaliar a adequação da linguagem.
- Confirmar informações contraditórias.
- Verificar a precisão de conteúdos jurídicos ou institucionais.
- Aprovar a comunicação antes de sua utilização.

O agente produz rascunhos e não possui autorização para enviar ou publicar conteúdos automaticamente.

## 7. Análise de riscos

### 7.1 Privacidade e LGPD

As solicitações corporativas podem conter dados pessoais ou informações confidenciais.

O uso dessas informações em serviços externos de processamento exige atenção à Lei Geral de Proteção de Dados Pessoais (Lei nº 13.709/2018).

Entre os riscos estão:

- Envio de dados pessoais desnecessários ao modelo.
- Exposição de informações confidenciais em documentos gerados.
- Acesso indevido às respostas armazenadas no Google Sheets.
- Compartilhamento inadequado de documentos no Google Docs.

Medidas preventivas propostas:

- Evitar inserir dados pessoais desnecessários nas solicitações.
- Não utilizar informações sensíveis em testes sem necessidade.
- Restringir o acesso às planilhas e documentos.
- Revisar as permissões das conexões utilizadas no Make.
- Avaliar as condições de privacidade e tratamento de dados dos serviços envolvidos.
- Definir políticas de retenção e descarte das informações.

A utilização dessas ferramentas não representa, por si só, uma certificação de conformidade com a LGPD. A organização responsável deve avaliar as bases legais, finalidades e condições de tratamento aplicáveis.

### 7.2 Alucinações

Alucinações acontecem quando o modelo apresenta informações incorretas ou não fundamentadas como se fossem verdadeiras.

No contexto do CorpAssist AI, isso pode ocorrer na criação de datas, nomes, decisões, participantes ou informações que não foram fornecidas.

Para reduzir esse risco, foram configuradas instruções que proíbem a criação de informações ausentes e exigem a sinalização de pendências.

Mesmo assim, a conferência humana continua indispensável.

### 7.3 Vieses

Modelos de linguagem podem reproduzir padrões discriminatórios ou interpretações inadequadas presentes nos dados utilizados em seu treinamento.

Em comunicações corporativas, isso pode resultar em linguagem excludente, tratamento desigual ou segmentação inadequada de públicos.

O agente possui instruções para sinalizar critérios de público potencialmente discriminatórios ou sem relação clara com a finalidade da comunicação.

A revisão humana também deve avaliar se o conteúdo respeita a diversidade, a igualdade de tratamento e as políticas da organização.

### 7.4 Segurança das informações

A integração entre Google Forms, Google Sheets, Make e Google Docs envolve conexões autenticadas e dados armazenados em serviços externos.

Os principais riscos são:

- Compartilhamento indevido de documentos.
- Exposição de credenciais e tokens de autenticação.
- Acesso não autorizado às planilhas.
- Uso inadequado de informações corporativas.
- Configuração incorreta das permissões das integrações.

Como medidas preventivas, recomenda-se utilizar conexões autenticadas, proteger credenciais, restringir permissões ao mínimo necessário e evitar armazenar tokens ou senhas em arquivos públicos do projeto.

## 8. Uso responsável da Inteligência Artificial

O CorpAssist AI foi desenvolvido considerando a IA como ferramenta de apoio, e não como substituta da responsabilidade humana.

O agente automatiza a interpretação e a elaboração inicial dos textos, mas não toma decisões institucionais, não aprova comunicações e não realiza envios automáticos.

A participação humana permanece necessária para validar informações, avaliar riscos e autorizar a utilização do conteúdo.

Essa abordagem busca equilibrar produtividade, qualidade e segurança no uso da Inteligência Artificial Generativa.

## 9. Considerações finais

O desenvolvimento do CorpAssist AI permitiu aplicar conceitos de Inteligência Artificial Generativa, engenharia de prompts, agentes de IA e automação em uma situação relacionada ao ambiente profissional.

A solução demonstra que um modelo de linguagem pode ser integrado a um fluxo automatizado para executar tarefas reais, interpretando informações estruturadas e produzindo conteúdos contextualizados.

Os testes também demonstraram a importância de aprimorar continuamente as instruções e avaliar criticamente os resultados gerados.

Conclui-se que a utilização responsável da IA depende não apenas da capacidade do modelo, mas também da qualidade das informações recebidas, das regras estabelecidas, da segurança das integrações e da supervisão humana.

## 10. Fontes de pesquisa

- Disciplina: Fundamentos de IA com Foco em IA Generativa.
- OpenAI — Documentação de modelos e conceitos de IA Generativa: https://platform.openai.com/docs
- Make — Documentação de automação e AI Agents: https://help.make.com
- Google AI for Developers — Gemini: https://ai.google.dev
- Anthropic — Documentação do Claude: https://docs.anthropic.com
- Brasil — Lei Geral de Proteção de Dados Pessoais (Lei nº 13.709/2018): https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm