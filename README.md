# M3sec

**Digital cleaning e proteção de dados pessoais**
Desindexação e remoção de informações pessoais em bases jurídicas e motores de busca, com fundamento em LGPD e legislação processual.

---

## Sumário

- [1. Posicionamento](#1-posicionamento)
- [2. Fundamentos jurídicos](#2-fundamentos-jurídicos)
- [3. Arquitetura de alvos](#3-arquitetura-de-alvos)
- [4. Matriz de triagem](#4-matriz-de-triagem)
- [5. Fluxo operacional](#5-fluxo-operacional)
- [6. Política de recusa](#6-política-de-recusa)
- [7. Precificação](#7-precificação)
- [8. Documentação obrigatória](#8-documentação-obrigatória)
- [9. Estrutura jurídica e compliance](#9-estrutura-jurídica-e-compliance)
- [10. Modelo financeiro](#10-modelo-financeiro)
- [11. Indicadores](#11-indicadores)
- [12. Roadmap de sistema](#12-roadmap-de-sistema)
- [13. Glossário](#13-glossário)

---

## 1. Posicionamento

### O que a M3sec faz

Diagnostica a exposição digital de uma pessoa ou empresa, classifica cada item encontrado por probabilidade real de remoção e executa as solicitações cabíveis nas três camadas (fonte, plataforma, indexador), com acompanhamento e monitoramento contínuo.

### O que a M3sec NÃO faz

Esta lista é parte da oferta, não uma ressalva. Ela deve aparecer no site, na proposta comercial e no contrato.

- **Não remove matéria jornalística verdadeira e licitamente publicada.** Não existe "direito ao esquecimento" no ordenamento brasileiro (ver seção 2).
- **Não promete resultado.** Vende tentativa qualificada com preço vinculado a êxito.
- **Não atua sobre dados de terceiros.** Somente o próprio titular, mediante verificação de identidade.
- **Não aceita casos da Faixa D** (seção 6), independentemente do valor oferecido.
- **Não opera credenciais gov.br do cliente.** O cliente assina no próprio dispositivo.

### Diferencial

Em um mercado onde os concorrentes prometem apagar tudo, o ativo da M3sec é **taxa de êxito comprovada e honestidade sobre o que não sai**. O relatório de diagnóstico que recusa cobrar por itens irremovíveis é a principal peça de conversão.

---

## 2. Fundamentos jurídicos

### 2.1 O que NÃO sustenta a operação

**Direito ao esquecimento — inexistente.**
STF, RE 1.010.606, Tema 786 (repercussão geral, acórdão publicado em 20/05/2021, rel. Min. Dias Toffoli):

> É incompatível com a Constituição a ideia de um direito ao esquecimento, assim entendido como o poder de obstar, em razão da passagem do tempo, a divulgação de fatos ou dados verídicos e licitamente obtidos e publicados em meios de comunicação social analógicos ou digitais.

Qualquer material de marketing que invoque "lei do esquecimento" configura oferta de serviço inexistente, com exposição no CDC (arts. 30 e 37). **Vedado.**

### 2.2 O que sustenta a operação

| Fundamento | Base legal | Aplicação |
|---|---|---|
| **Desindexação** | Não abarcada pelo Tema 786 — o julgamento expressamente não tratou do tema | Núcleo argumentativo da casa: pede-se desindexação **por nome**, não apagamento do fato |
| Direitos do titular | LGPD art. 18 (II correção, IV anonimização/bloqueio/eliminação, § 2º oposição) | Pedido administrativo a plataformas |
| Dados sensíveis | LGPD arts. 5º, II e 11 | Saúde, sexualidade, religião, biometria |
| Dados de menores | LGPD art. 14; ECA arts. 17 e 143 | Prioridade máxima; alta taxa de êxito |
| Segredo de justiça | CPC art. 189 | Família, sigilo decretado, interesse público |
| Sigilo de condenação | LEP art. 202; CP art. 93 (reabilitação) | Pena extinta ou cumprida; fundamento subutilizado no mercado |
| Conteúdo íntimo | Marco Civil art. 21; Lei 13.718/2018 | Remoção independe de ordem judicial |
| Dados de contato | Política de remoção do Google | Endereço, telefone, e-mail, documentos |

### 2.3 O que a jurisprudência contraria

Decisões dominantes reconhecem a licitude da divulgação, por provedores de aplicação, de conteúdo de processos judiciais não sigilosos, extraídos de diários oficiais. Consequência prática: **pedido genérico de remoção de processo público tende a falhar.** Sem triagem, a empresa cobra por fracasso.

> **Nota de manutenção:** revisar esta seção trimestralmente. Há movimentação regulatória ativa no CNJ e litígio em curso sobre agregadores de dados processuais.

---

## 3. Arquitetura de alvos

Toda remoção é atacada em três camadas, **sempre de cima para baixo**:

```
[1] FONTE — Tribunal / Diário Oficial
     Decretação de segredo, correção de classificação
     → única remoção definitiva
              │
              ▼
[2] PLATAFORMA — Jusbrasil, Escavador, agregadores
     Formulário administrativo, LGPD art. 18
              │
              ▼
[3] INDEXADOR — Google, Bing
     Desindexação de URL
```

**Erro crítico a evitar:** atacar o indexador primeiro. A URL sai da busca e retorna na varredura seguinte, porque a fonte continua publicando. Se a fonte é atacável, ela é o passo 1.

---

## 4. Matriz de triagem

### Faixas

| Faixa | Êxito esperado | Regra comercial |
|---|---|---|
| **A — Verde** | 80–95% | Aceitar. Prazo prometido. |
| **B — Amarelo** | 45–75% | Aceitar com prognóstico escrito. Êxito parcial é resultado válido. |
| **C — Laranja** | 15–40% | Aceitar somente com termo de ciência. Sem promessa. Cobrança só por êxito. |
| **D — Vermelho** | <10% | **Recusar.** Sem cobrança. |

### Faixa A — alta probabilidade

| Tipo de conteúdo | Fundamento | Alvo prioritário | Prazo |
|---|---|---|---|
| Processo em segredo de justiça indevidamente indexado | CPC art. 189 | Tribunal → plataforma → Google | 5–20 dias |
| Dados de criança/adolescente (ato infracional, guarda, adoção) | ECA arts. 17, 143; LGPD art. 14 | Plataforma | 2–10 dias |
| Ação de família (divórcio, alimentos, guarda, paternidade) | CPC art. 189, II | Tribunal → plataforma | 10–30 dias |
| Dados sensíveis (saúde, transtorno, interdição, orientação sexual, religião) | LGPD arts. 5º, II e 11 | Plataforma → Google | 10–30 dias |
| Conteúdo íntimo não consensual | Marco Civil art. 21 | Hospedeiro → Google | 24h–7 dias |
| Dados de contato (endereço, telefone, e-mail, CPF, RG) | LGPD art. 18 | Google → site fonte | 3–15 dias |
| Homônimo — processo de terceiro atribuído ao cliente | LGPD art. 18, III | Plataforma | 5–15 dias |
| Processo já excluído na fonte, ainda em cache/índice | LGPD art. 18, IV | Google | 3–10 dias |

### Faixa B — probabilidade média

| Tipo de conteúdo | Fundamento | Alvo | Condição para manter em B |
|---|---|---|---|
| Criminal com absolvição transitada em julgado | CP art. 93; desindexação | Tribunal → plataforma → Google | Certidão de trânsito em julgado. Sem ela → C |
| Inquérito arquivado sem denúncia | Ausência de acusação formal | Plataforma → Google | Certidão de arquivamento |
| Pena cumprida ou extinta há +2 anos | LEP art. 202 | Tribunal → plataforma | Certidão de extinção de punibilidade |
| Reclamação trabalhista com o cliente como **reclamante** | Vedação do CNJ à busca por nome de parte | Plataforma → Google | Há precedente favorável |
| Matéria jornalística com erro factual comprovado | Ilicitude do conteúdo (fora do Tema 786) | Veículo → Google | Prova documental do erro |
| Dados profissionais agregados (currículo, vínculos societários) | LGPD art. 18, § 2º | Plataforma | Depende de política interna |
| Cível encerrado com sentença favorável | Desindexação + desatualização | Plataforma → Google | Certidão de trânsito |

### Faixa C — baixa probabilidade

| Tipo de conteúdo | Por que é difícil | Oferta alternativa |
|---|---|---|
| Cível comum em andamento (cobrança, consumidor, execução) | Informação pública lícita | Monitoramento + supressão de SEO |
| Criminal em andamento | Interesse público, sem trânsito | Monitoramento apenas |
| Empresa como reclamada em ações trabalhistas | Sem proteção aplicável | Gestão de reputação |
| Execução fiscal / dívida ativa | Publicidade legalmente obrigatória | Regularização na origem |
| Falência e recuperação judicial | Publicidade é função do instituto | Recusar |
| Menções em redes sociais e fóruns | Fora do escopo LGPD-processual | Notificação extrajudicial caso a caso |

### Faixa D — recusar

| Tipo de conteúdo | Motivo |
|---|---|
| Matéria jornalística verdadeira e lícita | Tema 786 do STF — impossível de entregar |
| Condenação criminal transitada, sem reabilitação | Interesse público subsistente |
| Improbidade administrativa de agente público | Interesse público qualificado |
| Atos de agente público no exercício da função | CF art. 37 — princípio da publicidade |
| Fato sobre candidato ligado à aptidão para o cargo | Interesse público eleitoral |
| Condenação por crime contra criança, violência doméstica ou sexual | Recusa ética inegociável |
| Pedido de terceiro sobre dados alheios | Ilegal e tecnicamente inviável |

---

## 5. Fluxo operacional

### Fase 0 — Qualificação (gratuita, 10 min)

Contato inicial. Confirmar que o solicitante é o titular. Identificar se há indício de Faixa D. **Encerrar aqui se houver.**

### Fase 1 — Diagnóstico (pago, 48h)

1. Varredura do nome, CPF/CNPJ e variações em: Google, Bing, Jusbrasil, Escavador, agregadores secundários, consultas públicas dos tribunais competentes.
2. Registro de cada item: URL, título, fonte, print datado, natureza do conteúdo.
3. Classificação individual por faixa, com fundamento nomeado.
4. Identificação da camada de ataque de cada item.
5. **Entregável:** Relatório de Diagnóstico com item-a-item, faixa, fundamento, prognóstico e preço. Itens de Faixa D aparecem no relatório, marcados como não executáveis e **sem cobrança**.

### Fase 2 — Contratação

Contrato de prestação de serviços + procuração específica por plataforma + Termo de Ciência de Prognóstico (assinado item a item). Cliente assina no próprio dispositivo.

### Fase 3 — Execução

Por item, na ordem fonte → plataforma → indexador. Protocolo registrado com número, data e canal. Cada item vira um card com status:

`TRIADO` → `PROTOCOLADO` → `EM ANÁLISE` → `DEFERIDO` / `INDEFERIDO` → `VERIFICADO` → `ENCERRADO`

### Fase 4 — Acompanhamento

Recontato conforme SLA. Indeferimento administrativo aciona decisão: recurso, escalonamento jurídico (via advogado parceiro) ou encerramento com devolução de expectativa.

### Fase 5 — Verificação

Confirmação de que o item saiu de fato, em busca anônima (janela privativa, sem histórico). Print datado do antes e depois. **Só há êxito — e cobrança de êxito — após verificação.**

### Fase 6 — Encerramento

Relatório final com resultado por item, taxa de êxito do caso e recomendação de monitoramento.

### Fase 7 — Monitoramento (recorrente)

Varredura periódica. Alerta de reaparecimento ou item novo. Reexecução inclusa conforme plano.

### SLA por faixa

| Faixa | Primeira resposta | Prazo de execução | Frequência de acompanhamento |
|---|---|---|---|
| A | 24h | 30 dias | Semanal |
| B | 48h | 60 dias | Quinzenal |
| C | 72h | 90 dias | Mensal |

---

## 6. Política de recusa

Regra vinculante. Vale para todo membro da equipe, sem exceção por valor de contrato.

**Recusa automática quando:**

1. O solicitante não é o titular dos dados.
2. O conteúdo se enquadra em qualquer linha da Faixa D.
3. Há indício de que a remoção visa lesar terceiro (ocultar histórico antes de negócio, contratação, relacionamento ou crédito).
4. Há processo criminal em andamento por fraude, estelionato ou crime patrimonial e o pedido recai sobre ele.
5. O cliente pressiona por garantia de resultado após esclarecimento.

**Registro:** toda recusa é documentada com data, motivo e enquadramento. O registro protege a empresa e alimenta o argumento comercial.

**Risco a mitigar:** neste nicho, o cliente que paga melhor pode ser exatamente aquele cuja exposição serve ao interesse público. Uma reportagem sobre "empresa que apaga o passado de criminosos" encerra a M3sec. A política de recusa não é moralismo — é continuidade do negócio.

---

## 7. Precificação

| Faixa | Diagnóstico | Execução | Êxito (por item) |
|---|---|---|---|
| A | R$ 197 | incluído | R$ 400–900 |
| B | R$ 197 | R$ 300 | R$ 800–2.000 |
| C | R$ 197 | somente êxito | R$ 1.500+ |
| D | **R$ 0** | — | — |

**Monitoramento:** R$ 49–99/mês (pessoa física) · R$ 300–900/mês (empresa)

**Princípios:**
- O diagnóstico é sempre pago — filtra curioso e cobre o custo real da varredura.
- Nunca cobrar por item de Faixa D. É investimento de credibilidade.
- Êxito só é faturado após verificação (Fase 5).
- Remoção é evento único; **o recorrente é o monitoramento**. A saúde financeira da empresa depende dele.

---

## 8. Documentação obrigatória

Por caso, sem exceção:

- [ ] Documento de identidade e CPF/CNPJ do titular
- [ ] Comprovante de verificação de identidade
- [ ] Procuração específica, com poderes descritos por plataforma
- [ ] Certidões de fundamento (trânsito em julgado, arquivamento, extinção de punibilidade, decreto de segredo)
- [ ] Print + URL + data de cada item, no diagnóstico
- [ ] Termo de Ciência de Prognóstico, assinado item a item
- [ ] Protocolos de todas as solicitações
- [ ] Print de verificação pós-remoção
- [ ] Registro de recusas, quando aplicável

---

## 9. Estrutura jurídica e compliance

### Pré-requisitos antes do primeiro caso

| Item | Situação |
|---|---|
| CNPJ e enquadramento tributário | ☐ |
| Contrato de prestação de serviços revisado por advogado | ☐ |
| Modelo de procuração específica | ☐ |
| Termo de Ciência de Prognóstico | ☐ |
| Parceria formalizada com advogado ou sociedade de advogados | ☐ |
| Política de privacidade e registro de tratamento (LGPD) | ☐ |
| Encarregado de dados (DPO) designado | ☐ |
| Seguro de responsabilidade civil profissional | ☐ |
| Registro de marca no INPI | ☐ |

### Fronteira OAB

- **Permitido à M3sec:** pedido administrativo com base na LGPD, diagnóstico, monitoramento, gestão documental.
- **Privativo de advogado:** petição judicial, pedido de liminar, ação de obrigação de fazer, requerimento de segredo de justiça em juízo.

Onde o caso exige judicialização, o encaminhamento é ao advogado parceiro, com contrato próprio. Atenção às restrições da OAB quanto a captação de clientela e publicidade — o material de marketing da M3sec não pode se apresentar como escritório.

### gov.br

A assinatura eletrônica gov.br é **pessoal e intransferível**. A M3sec jamais acessa, armazena ou opera credenciais do cliente. No atendimento presencial, o cliente assina no próprio dispositivo, com registro de consentimento.

### A M3sec como controladora de dados

Ironia operacional a levar a sério: a empresa acumula dossiês de dados sensíveis de pessoas que a procuraram justamente por exposição. Um vazamento aqui é fatal. Requisitos mínimos: criptografia em repouso, controle de acesso por função, log de acesso, política de retenção com descarte definido e proibição de armazenamento em dispositivos pessoais.

---

## 10. Modelo financeiro

> Números ilustrativos para modelagem — substituir por cotações reais antes de qualquer decisão.

### Estrutura de custo

| Natureza | Item |
|---|---|
| Fixo | Abertura e contabilidade, ferramentas de monitoramento, jurídico consultivo, infraestrutura |
| Variável por caso | Custas e certidões, horas de execução, comissão do advogado parceiro nos casos judicializados |
| Aquisição | Tráfego pago, comissão de canal (escritórios parceiros) |

### Unidade de análise: o caso

```
Receita do caso = Diagnóstico + Σ(êxitos por item) + LTV do monitoramento
Margem          = Receita − (custas + horas + comissão de canal)
```

**Métrica-chave do modelo:** *itens de Faixa A e B por caso.* Um caso com 6 itens verdes vale muito mais que dois casos com 1 item laranja cada — e custa quase o mesmo para atender. A triagem não é só proteção jurídica: é o mecanismo de seleção de rentabilidade.

### Ponto de equilíbrio

Calcular com dados reais após os 10 primeiros casos. Antes disso, qualquer projeção é ficção.

---

## 11. Indicadores

**Operacionais**
- Taxa de êxito global e por faixa
- Prazo médio até deferimento, por camada e por plataforma
- Aderência ao SLA
- Itens por caso e distribuição entre faixas

**Comerciais**
- Conversão qualificação → diagnóstico
- Conversão diagnóstico → contratação
- Ticket médio
- Adesão ao monitoramento (**o número que define a sustentabilidade**)
- Churn do monitoramento
- CAC por canal

**Risco**
- Recusas registradas, por motivo
- Reclamações e chargebacks
- Taxa de reaparecimento de item removido

### Calibração da matriz

A cada 20 casos, comparar êxito real vs. faixa atribuída. Divergência acima de 20% em qualquer faixa exige reclassificação daquele tipo de conteúdo. **A matriz é viva — este README é o documento de versão dela.**

---

## 12. Roadmap de sistema

> **Regra:** nada de software antes de 20 casos rodados manualmente. Processo instável vira retrabalho.

### Fase 0 — Manual (casos 1 a 20)

Planilha de triagem, modelos de documento, drive organizado por caso, calendário de acompanhamento. O objetivo é descobrir onde o processo quebra.

### Fase 1 — Sistema interno

CRM de casos com kanban por status, biblioteca de fundamentos, geração de relatório de diagnóstico, controle de protocolos e SLA, dashboard de indicadores.

### Fase 2 — Monitoramento automatizado

Varredura periódica agendada, detecção de item novo ou reaparecido, alerta ao cliente. **É aqui que existe automação real e defensável.**

### Fase 3 — Portal do cliente

Acompanhamento de status por item, upload de documentos, assinatura de termos, histórico e relatórios.

### Fase 4 — Automação de solicitações — VALIDAR ANTES

⚠️ **Premissa não confirmada.** Não há evidência de API pública de remoção em Jusbrasil, Escavador ou Google — existem formulários. A ferramenta do Google exige verificação de identidade justamente para impedir que terceiros solicitem remoção em nome de outrem.

**Antes de planejar esta fase:** contatar as três plataformas e obter resposta formal sobre existência de API ou canal de parceria, e ler os termos de uso quanto a acesso automatizado. Se a resposta for negativa, o produto correto é fluxo assistido — a M3sec prepara, o cliente conclui com um clique.

---

## 13. Glossário

| Termo | Definição |
|---|---|
| **Item** | Uma URL individual a ser tratada. Unidade de trabalho e de cobrança. |
| **Caso** | Conjunto de itens de um mesmo titular. |
| **Camada** | Fonte, plataforma ou indexador. |
| **Faixa** | Classificação A/B/C/D por probabilidade de êxito. |
| **Verificação** | Confirmação em busca anônima de que o item saiu. Condição para faturar êxito. |
| **Desindexação** | Retirada da URL dos resultados de busca, sem remoção do conteúdo na origem. |

---

## Ordem de execução recomendada

1. Estrutura jurídica completa (seção 9) — **bloqueia tudo o mais**
2. Modelos de documento: contrato, procuração, termo de ciência, relatório
3. Planilha de triagem e drive de casos
4. Casos 1 a 5 — gratuitos ou a preço de custo, com foco em aprendizado
5. Calibração da matriz e do modelo financeiro com dados reais
6. Casos 6 a 20 — preço cheio, medindo tudo
7. Sistema interno (Roadmap Fase 1)
8. **Só então:** posicionamento, site e plano de marketing

---

**Licença:** conteúdo interno. Não distribuir.
**Versão:** 1.0 — agosto/2026
