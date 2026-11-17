# CorpAssist AI

> Assistente de IA generativa que transforma um formulário em um **rascunho de comunicação corporativa pronto para revisão**, sem código e sem envio automático.

## 📊 Resultados e impacto

| Indicador | Resultado |
|---|---|
| Tipos de comunicação suportados | **6** (e-mail, comunicado, resumo, ata, mensagem, revisão de texto) |
| Cenários de teste integrado executados | **7** |
| Etapas manuais entre o pedido e o rascunho | **0** (formulário → documento, tudo automatizado) |
| Latência máxima de entrada no fluxo | **até 15 min** (polling do Make) |
| Comunicações enviadas/publicadas sem aprovação | **0** (revisão humana obrigatória por design) |
| Ferramentas pagas de infraestrutura próprias | **0** (Google Workspace + Make + API do modelo) |

### Tempo economizado

Comparação entre o tempo manual típico (referências de mercado) e o tempo com o CorpAssist AI, **incluindo a revisão humana**.

| Tipo | Manual (referência) | Com CorpAssist (incl. revisão) | Redução estimada |
|---|---|---|---|
| E-mail corporativo | ~6 min | 3 min | 48% |
| Ata de reunião (reunião de 60 min) | 20–30 min | < 5 min | 75–83% |
| Comunicado interno | ~2 h (comunicado de maior porte) | < 5 min | 96% |

### Qualidade: o que os testes demonstraram

| Cenário testado | Comportamento verificado | Evidência |
|---|---|---|
| Resumo de reunião com informações incompletas | Não inventou decisões; sinalizou lacunas | `evidencias/` |
| Revisão de texto sobre LGPD | Preservou o sentido e o formato original | `evidencias/teste-revisao.png` |
| E-mail sobre mudança de horário | Estrutura adequada ao tipo e ao público | `evidencias/teste-email.png` |
| Comunicado de manutenção programada | Tom e formatação padronizados | `evidencias/` |
| Ata com decisões e pendências | Separou fatos, decisões e pendências; sem participantes inventados | `evidencias/teste-ata.png` |
| Mensagem sobre férias | Adequação ao canal e ao tom | `evidencias/teste-mensagem.png` |
| Texto com regras contraditórias (presencial/remoto/híbrido) | **Identificou a contradição** e pediu confirmação, sem escolher uma versão | `evidencias/teste-revisao.png` |

**Melhoria iterativa:** as instruções do agente foram refinadas durante a validação para reduzir inferências indevidas, eliminar informações inventadas e padronizar a formatação.

## 🎯 Problema

Redigir comunicações corporativas consome tempo e costuma gerar inconsistências de tom, de estrutura e de informação. Ferramentas de IA genéricas resolvem a velocidade, mas introduzem um risco: **inventar nomes, datas e decisões**.

## 💡 Solução

O CorpAssist AI coleta o pedido de forma estruturada (tipo, objetivo, público, canal, tom, informações e observações) e gera um rascunho com regras rígidas de **fidelidade às informações**:

- não inventa nomes, datas, cargos, valores ou decisões;
- usa marcadores editáveis quando falta informação;
- sinaliza ambiguidades e contradições em vez de escolher uma interpretação;
- gera somente rascunhos, e a aprovação humana é obrigatória.

## 🏗️ Arquitetura

```
Google Forms → Google Sheets → Make (Watch New Rows) → Make AI Agent (Claude Haiku 4.5) → Google Docs → Revisão humana
```

| Ferramenta | Função |
|---|---|
| Google Forms | Coleta estruturada das solicitações |
| Google Sheets | Armazenamento das respostas |
| Make | Orquestração e automação (verificação a cada 15 min) |
| Make AI Agent + Claude Haiku 4.5 | Interpretação do pedido e geração do texto |
| Google Docs | Armazenamento dos documentos gerados |

## 🧠 Decisões de projeto

- **Human-in-the-loop obrigatório:** o sistema nunca envia nem publica nada sozinho.
- **Formulário estruturado:** reduz pedidos vagos e melhora a consistência da saída.
- **Prompt orientado a fidelidade:** regras específicas para ambiguidade, atas e revisão (não transformar revisão em e-mail, não deduzir datas relativas).
- **Modelo leve (Haiku 4.5):** equilíbrio entre custo e velocidade para texto corporativo.
- **Minimização de dados:** o agente evita solicitar dados pessoais desnecessários.

## 🖼️ Evidências

| | |
|---|---|
| Formulário de entrada | `evidencias/formulario.png` |
| Planilha de respostas | `evidencias/google-sheets.png` |
| Cenário de automação | `evidencias/workflow-make.png` |
| Configuração do agente | `evidencias/agente-ia.png` |
| E-mail gerado | `evidencias/teste-email.png` |
| Ata gerada | `evidencias/teste-ata.png` |
| Revisão com contradições | `evidencias/teste-revisao.png` |
| Mensagem corporativa | `evidencias/teste-mensagem.png` |

## ▶️ Como usar

1. Acesse o formulário e escolha o tipo de comunicação.
2. Informe objetivo, público, canal e tom.
3. Preencha as informações principais e observações.
4. Envie e aguarde o processamento (até 15 min).
5. Abra o documento no Google Docs, **revise e aprove** antes de usar.

🔗 **Acesso:** [Formulário](GOOGLE_FORMS_URL) · [Planilha](GOOGLE_SHEETS_URL) · [Cenário Make](MAKE_URL) · [Documentos de demonstração](DOCS_URL)

## ⚠️ Limitações

- O modelo pode interpretar mal ou deixar passar inconsistências.
- O conteúdo gerado **não é uma comunicação oficial** até ser aprovado por uma pessoa.
- Revisão redobrada em conteúdo com dados pessoais, informações confidenciais, decisões organizacionais ou orientação jurídica.
- Latência de até 15 min por causa do polling do Make.

