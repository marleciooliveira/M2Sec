# M2Sec — Avaliação de Patrimônio

> **Rascunho — não é laudo de avaliação formal.** Para uso em entrada de sócio, declaração contábil oficial, negociação de venda ou captação de investimento, é necessário um contador ou avaliador certificado assinando em cima destes números. Serve como rascunho estruturado e ponto de partida.

- **Data:** 16 de setembro de 2026
- **Empresa:** M2Sec (ex-M3sec)
- **Preparado por:** levantamento assistido, a partir de dados informados pelo fundador (Marlécio Oliveira)
- **Versão:** 1.0
- **Versão visual (artifact publicado):** https://claude.ai/code/artifact/6e201366-74ed-40bf-bf8c-1779deff8ee0

---

## 1. Sumário executivo

**Patrimônio estimado (custo de reposição): R$ 171.726**

Mão de obra especializada (R$ 100/hora geral + R$ 129/hora para DevOps/DevSecOps, taxa pesquisada de mercado) + setup legal e domínios. Não inclui infraestrutura em nuvem, que é despesa operacional recorrente, não patrimônio — ver seção 5. Fontes de cada número na seção 7.

| | Valor |
|---|---:|
| Já construído (230h) | R$ 23.000 |
| Falta construir (1.370h) | R$ 148.310 |
| Opex AWS produção (500–1.000 usuários) | R$ 2.880–4.560/mês (R$ 34.500–54.700/ano) — não entra no total acima |

A taxa de R$ 100/hora (trabalho geral) foi definida pelo fundador; a taxa de R$ 129/hora (DevOps/DevSecOps) vem de pesquisa de salário de mercado para profissional sênior no Brasil — ver seção 7. A seção 6 mostra o mesmo levantamento com taxas de mercado pesquisadas em todas as frentes, para referência — o intervalo entre metodologias vai de **R$ 172 mil a R$ 193 mil**.

---

## 2. Metodologia

Empresa pré-receita, sem faturamento nem usuários pagantes até o momento — por isso o método aplicável é **custo de reposição** (quanto custaria pagar terceiros para recriar tudo do zero), não múltiplo de faturamento ou fluxo de caixa descontado.

- Horas por frente de trabalho estimadas com base no escopo real do projeto (pesquisa já existente, README/plano de marketing, landing page publicada, e o que falta: app, backend, automação, infraestrutura).
- Taxa horária de R$ 100 (geral, definida pelo fundador) e R$ 129 (DevOps/DevSecOps, pesquisada em fontes de mercado — seção 7) aplicadas conforme a frente de trabalho.
- Itens marcados **estimado** ainda não têm valor real informado e usam preço de mercado — devem ser substituídos pelos valores reais antes de qualquer uso formal do documento.
- Infraestrutura em nuvem é despesa recorrente (opex), não patrimônio — reportada separadamente.

---

## 3. Mão de obra especializada

Taxa geral de R$ 100/hora (definida pelo fundador) para concepção, produto e desenvolvimento. Frentes de DevOps/DevSecOps usam R$ 129/hora — taxa pesquisada a partir de salário de mercado para profissional sênior no Brasil (seção 7).

| Frente de trabalho | Horas | R$/hora | Situação | Valor |
|---|---:|---:|---|---:|
| Concepção do modelo de negócio, pesquisa de nicho, base jurídica (LGPD, Tema 786) | 120h | 100 | concluído | R$ 12.000 |
| Identidade de marca, design system, landing page | 60h | 100 | concluído | R$ 6.000 |
| Documentação técnica e operacional (README, SLAs, matriz de triagem) | 50h | 100 | concluído | R$ 5.000 |
| Arquitetura e implantação de infraestrutura AWS (VPC, EC2, ALB, Auto Scaling, RDS, WAF) `devops` | 180h | 129 | a fazer | R$ 23.220 |
| DevSecOps — hardening, IAM, backup/DR, monitoramento, resposta a incidente `devops` | 140h | 129 | a fazer | R$ 18.060 |
| Backend e automação do sistema gestor (triagem, notificações, case tracking, API) | 400h | 100 | a fazer | R$ 40.000 |
| Aplicativo mobile (solicitação e acompanhamento de remoção) | 500h | 100 | a fazer | R$ 50.000 |
| Integração de gateway de pagamento + emissão fiscal (NF-e) | 80h | 100 | a fazer | R$ 8.000 |
| Automação de builds / pipelines CI-CD `devops` | 70h | 129 | a fazer | R$ 9.030 |
| **Total** | **1.600h** | | | **R$ 171.310** |

Linhas marcadas `devops` usam a taxa pesquisada de mercado (390h × R$ 129/h = R$ 50.310); as demais usam a taxa geral definida (1.210h × R$ 100/h = R$ 121.000).

---

## 4. Setup legal e domínios

Valores reais ainda não informados — usando estimativas até confirmação.

| Item | Situação | Valor |
|---|---|---:|
| CNPJ + alvará (coordenação contábil, 3h à taxa geral de R$ 100/h) | estimado | R$ 300 |
| m3sec.com.br — registro (Registro.br) | estimado | R$ 40/ano |
| m2sec.com.br — reativação (Registro.br) | estimado | R$ 76/ano |
| **Total** | | **R$ 416** |

Confirmado nesta sessão: m2sec.com.br publicado e válido até 30/07/2027; m3sec.com.br publicado e válido até 24/11/2026; repositório de código migrado para `github.com/marleciooliveira/M2Sec`.

---

## 5. Infraestrutura de produção — dimensionamento AWS

Dois cenários de pico — 500 e 1.000 usuários simultâneos — região São Paulo (sa-east-1), com WAF/Shield e banco de dados gerenciado (RDS Multi-AZ). Preços de tabela pública AWS — não foi possível consultar a conta real (sessão AWS expirada, ver seção 7); confirme no [AWS Pricing Calculator](https://calculator.aws) antes de orçar formalmente.

**Arquitetura:** Internet → AWS WAF + Shield Standard → Application Load Balancer → Auto Scaling (EC2 t3.large) → RDS Multi-AZ PostgreSQL, com S3 (evidências), NAT Gateway (2 AZs) e CloudWatch.

### Cenário A — até 500 usuários simultâneos

| Componente | Dimensionamento | US$/mês | R$/mês |
|---|---|---:|---:|
| EC2 (Auto Scaling Group) | t3.large, ~2 instâncias médias (pico 3) | 206 | 1.112 |
| Application Load Balancer | 1 ALB + LCUs | 55 | 297 |
| RDS PostgreSQL Multi-AZ | db.t3.small + 50GB gp3 | 82 | 443 |
| AWS WAF + regras gerenciadas | 1 Web ACL, ~10 regras | 17 | 92 |
| Shield Standard | incluso | 0 | 0 |
| NAT Gateway (2 AZs) | alta disponibilidade | 102 | 551 |
| S3 (evidências/documentos) | ~50GB + requisições | 5 | 27 |
| CloudWatch (logs/métricas/alarmes) | | 18 | 97 |
| Transferência de dados de saída | ~150GB/mês | 38 | 205 |
| Route 53 + backups (AWS Backup) | | 10 | 54 |
| **Total médio** | | **533** | **2.878** |

Pico sustentado 24h (sem auto-scaling reduzindo à noite): ≈ US$ 635/mês (R$ 3.429/mês, R$ 41.150/ano).

### Cenário B — até 1.000 usuários simultâneos

| Componente | Dimensionamento | US$/mês | R$/mês |
|---|---|---:|---:|
| EC2 (Auto Scaling Group) | t3.large, ~3,5 instâncias médias (pico 6) | 360 | 1.944 |
| Application Load Balancer | 1 ALB + LCUs | 75 | 405 |
| RDS PostgreSQL Multi-AZ | db.t3.medium + 100GB gp3 | 162 | 875 |
| AWS WAF + regras gerenciadas | 1 Web ACL, ~10 regras | 18 | 97 |
| Shield Standard | incluso | 0 | 0 |
| NAT Gateway (2 AZs) | alta disponibilidade | 108 | 583 |
| S3 (evidências/documentos) | ~100GB + requisições | 8 | 43 |
| CloudWatch (logs/métricas/alarmes) | | 25 | 135 |
| Transferência de dados de saída | ~300GB/mês | 75 | 405 |
| Route 53 + backups (AWS Backup) | | 13 | 70 |
| **Total médio** | | **844** | **4.558** |

Pico sustentado 24h (sem auto-scaling reduzindo à noite): ≈ US$ 1.101/mês (R$ 5.945/mês, R$ 71.300/ano).

Câmbio de referência usado nos dois cenários: R$ 5,40/US$ — confirme a cotação do dia antes de orçar formalmente.

---

## 6. Cenário alternativo — taxas de mercado por especialidade

Mesma lista de horas da seção 3, mas agora com **todas** as taxas pesquisadas em fontes de mercado (não só DevOps/DevSecOps) — ver fontes e cálculo na seção 7. Útil como teto de comparação com a taxa geral de R$ 100/hora definida pelo fundador.

| Frente de trabalho | Horas | R$/hora | Valor |
|---|---:|---:|---:|
| Pesquisa de negócio / compliance | 120h | 85 | R$ 10.200 |
| Marca / design | 60h | 109 | R$ 6.540 |
| Documentação | 50h | 69 | R$ 3.450 |
| Arquitetura AWS sênior | 180h | 129 | R$ 23.220 |
| DevSecOps sênior | 140h | 129 | R$ 18.060 |
| Backend / automação | 400h | 125 | R$ 50.000 |
| App mobile | 500h | 125 | R$ 62.500 |
| Gateway de pagamento | 80h | 125 | R$ 10.000 |
| CI/CD | 70h | 129 | R$ 9.030 |
| **Total (+ legal/domínios: R$ 416)** | **1.600h** | | **R$ 193.416** |

Com todas as taxas pesquisadas em fontes de mercado, o cenário alternativo caiu de R$ 289 mil (estimativas próprias anteriores) para **R$ 193.416** — mais perto do custo de reposição com taxa geral definida pelo fundador (R$ 171.726). A diferença entre os dois agora é de **R$ 21,7 mil**, quase toda concentrada na taxa geral de R$ 100/hora ficar levemente abaixo do mercado para backend, app mobile e design.

---

## 7. Referências e fontes

De onde vem cada número deste documento — para que qualquer valor possa ser conferido ou substituído.

| Bloco de valor | Fonte / base |
|---|---|
| Metodologia geral | Custo de reposição (replacement cost) — abordagem padrão para ativos intangíveis de empresas pré-receita, sem faturamento ou tração para justificar múltiplo de receita ou fluxo de caixa descontado. |
| Taxa horária geral — R$ 100/h | Definida por Marlécio Oliveira (fundador), não é benchmark de mercado. Aplicada às 1.210h de concepção, marca, documentação, backend, app e gateway (seção 3). |
| Taxa horária DevOps/DevSecOps — R$ 129/h | Pesquisada em 16/09/2026. Aplicada às 390h de arquitetura AWS, DevSecOps e CI/CD (seção 3). Fórmula de conversão e multiplicador de encargos são estimativa própria, não citação de terceiros — ajustável. Ver cálculo e fontes de salário abaixo. |
| Taxas de mercado — seção 6 | Faixas aproximadas observadas em plataformas de contratação PJ/freelancer sênior no Brasil (ex.: Workana, 99Freelas) e pesquisas de remuneração de TI (ex.: Robert Half, Michael Page Brasil). Sem fonte única auditável — validar antes de uso formal. |
| Preços de infraestrutura AWS — seção 5 | Tabela pública de preços on-demand da AWS para sa-east-1. Não foi possível autenticar na conta AWS real nesta sessão (token de login expirou antes da confirmação) — valores de conhecimento geral de tabela AWS, não de cotação ao vivo. Confirmar no [AWS Pricing Calculator](https://calculator.aws). |
| Câmbio USD/BRL — R$ 5,40 | Referência aproximada, set/2026. Confirmar cotação do dia (PTAX/Banco Central) antes de uso formal. |
| CNPJ, alvará, domínios — seção 4 | Valores estimados, pendentes do valor real pago — ver seção 8. |
| Status dos domínios | Consultado diretamente no painel Registro.br nesta sessão (16/09/2026): m2sec.com.br publicado até 30/07/2027; m3sec.com.br publicado até 24/11/2026. |

### Cálculo da taxa DevOps/DevSecOps (R$ 129/h)

Pesquisa de salário de DevOps no Brasil, realizada em 16/09/2026:

| Fonte | Cargo/nível | Salário mensal (BRL) | Link |
|---|---|---:|---|
| Glassdoor Brasil | Senior DevOps Engineer (usado no cálculo) | R$ 13.750 | https://www.glassdoor.com.br/Sal%C3%A1rios/senior-devops-engineer-sal%C3%A1rio-SRCH_KO0,22.htm |
| Trybe (guia de salários) | DevOps sênior (usado no cálculo) | R$ 12.049,50 | https://www.betrybe.com/guia-salarios-profissoes/devops |
| Glassdoor Brasil | DevOps Engineer, geral (referência cruzada) | R$ 9.091 | https://www.glassdoor.com.br/Sal%C3%A1rios/devops-engineer-sal%C3%A1rio-SRCH_KO0,15.htm |
| Glassdoor Brasil | Engenheiro De DevOps, geral (referência cruzada) | R$ 8.333 | https://www.glassdoor.com.br/Sal%C3%A1rios/engenheiro-de-devops-sal%C3%A1rio-SRCH_KO0,20.htm |
| Glassdoor Brasil | DevOps Engineer, São Paulo (referência cruzada) | R$ 10.100 | https://www.glassdoor.com.br/Sal%C3%A1rios/s%C3%A3o-paulo-devops-engineer-sal%C3%A1rio-SRCH_IL.0,9_IS3937_KO10,25.htm |
| Salário Transparente | DevOps Pleno (referência cruzada) | R$ 9.442 | https://salariotransparente.com.br/salarios/devops/pleno |
| Indeed Brasil | DevOps, geral (referência cruzada, sem valor mensal limpo extraído) | — | https://br.indeed.com/career/devops/salaries |
| Indeed Brasil | Engenheiro de DevOps (referência cruzada, sem valor mensal limpo extraído) | — | https://br.indeed.com/career/engenheiro-de-devops/salaries |

**Fórmula aplicada** (nível sênior, por ser o perfil de trabalho descrito nas frentes de arquitetura/segurança):

```
Média salarial sênior = (R$ 13.750 + R$ 12.049,50) / 2 = R$ 12.899,75/mês
Taxa PJ/hora = (salário × 1,6 de encargos/benefícios) ÷ 160h/mês
            = (R$ 12.899,75 × 1,6) ÷ 160
            ≈ R$ 129/hora
```

O multiplicador de 1,6× e a jornada de 160h/mês são convenções comuns para converter salário CLT em taxa PJ/freelance no Brasil (cobrem 13º, FGTS, INSS patronal, férias e ausência de estabilidade que um contratante PJ precisa embutir no preço) — não são um dado de mercado citável, e podem ser ajustados.

As linhas "referência cruzada" não entraram no cálculo, mas mostram que R$ 129/h está acima da média geral de mercado (R$ 8.300–10.100/mês, perfil pleno) e coerente com a faixa sênior — o que é esperado, já que arquitetura de infraestrutura e hardening de segurança são trabalho sênior.

### Cálculo das demais taxas do cenário de mercado (seção 6)

Mesma pesquisa (16/09/2026), mesma fórmula (salário sênior × 1,6 ÷ 160h/mês), aplicada às outras frentes de trabalho:

| Frente | Fonte | Cargo/nível | Salário mensal (BRL) | Taxa/hora |
|---|---|---|---:|---:|
| Pesquisa de negócio / compliance | [Glassdoor Brasil](https://www.glassdoor.com.br/Sal%C3%A1rios/consultor-em-lgpd-sal%C3%A1rio-SRCH_KO0,17.htm) | Consultor em LGPD | R$ 8.500 | R$ 85 |
| Marca / design | [Glassdoor Brasil](https://www.glassdoor.com.br/Sal%C3%A1rios/designer-ui-ux-senior-sal%C3%A1rio-SRCH_KO0,21.htm), [2](https://www.glassdoor.com.br/Sal%C3%A1rios/senior-ux-ui-designer-sal%C3%A1rio-SRCH_KO0,21.htm), [3](https://www.glassdoor.com.br/Sal%C3%A1rios/senior-ui-designer-sal%C3%A1rio-SRCH_KO0,18.htm) | UI/UX Designer sênior (média de 3 variações de título: R$ 9.752 / R$ 8.775 / R$ 14.167) | R$ 10.898 | R$ 109 |
| Documentação | [Salário.com.br](https://www.salario.com.br/profissao/redator-de-textos-tecnicos-cbo-261530/) | Redator de Textos Técnicos, sênior | R$ 6.854,78 | R$ 69 |
| Backend / automação | [Glassdoor Brasil](https://www.glassdoor.com.br/Sal%C3%A1rios/desenvolvedor-backend-senior-sal%C3%A1rio-SRCH_KO0,28.htm) | Desenvolvedor Backend, sênior | R$ 12.500 | R$ 125 |
| App mobile | [Glassdoor Brasil](https://www.glassdoor.com.br/Sal%C3%A1rios/desenvolvedor-mobile-s%C3%AAnior-sal%C3%A1rio-SRCH_KO0,27.htm), [2](https://www.glassdoor.com.br/Sal%C3%A1rios/desenvolvedor-android-senior-sal%C3%A1rio-SRCH_KO0,28.htm), [3](https://www.glassdoor.com.br/Sal%C3%A1rios/senior-mobile-developer-sal%C3%A1rio-SRCH_KO0,23.htm) | Desenvolvedor Mobile sênior (média de 3 variações: R$ 12.208 / R$ 12.762 / R$ 12.550) | R$ 12.507 | R$ 125 |
| Gateway de pagamento | — | Sem cargo específico no mercado; assumido igual a Backend (integração de API é trabalho de backend) | — | R$ 125 |
| Arquitetura AWS / DevSecOps / CI-CD | ver tabela DevOps acima | Senior DevOps Engineer | R$ 12.899,75 | R$ 129 |

**Nota:** valores de designer, redator e desenvolvedor mobile são a média simples de duas ou três variações de título coletadas no Glassdoor para a mesma função, já que buscas com nomenclaturas diferentes (ex.: "UX UI Designer" vs. "Designer UI UX Senior") retornam amostras distintas.

---

## 8. Pendente de confirmação

Para fechar a versão final deste documento, ainda faltam estes valores reais:

- Valor efetivamente pago ao contador pela abertura do CNPJ + alvará (hoje estimado em R$ 300).
- Valor real pago em cada domínio — m3sec.com.br (registro original) e m2sec.com.br (reativação).
- Pagamentos a terceiros, se houve terceirização de alguma parte (design, dev, redação).
- Situação da marca "M2sec" no INPI — registrada, em processo, ou não iniciada. Se houver registro, soma valor de propriedade intelectual defensável ao patrimônio.
- Cotação AWS real (sessão da conta expirou nesta sessão) — os valores da seção 5 são de tabela pública, não da conta real.
