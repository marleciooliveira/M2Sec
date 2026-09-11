# Modelo de Negócio — M3Sec

Documento de discussão estratégica. Não é plano decidido, é ponto de partida pra conversa — mesmo espírito do `modelo-negocio.md` do projeto Imersão.

---

## Sumário

- [Tese central](#tese-central)
- [O risco de fundo: isso pode virar exercício ilegal da advocacia](#o-risco-de-fundo-isso-pode-virar-exercício-ilegal-da-advocacia)
- [Dividir o produto por camada jurídica](#dividir-o-produto-por-camada-jurídica)
- [Segmentação de mercado](#segmentação-de-mercado)
- [Panorama competitivo](#panorama-competitivo)
- [Modelo de monetização](#modelo-de-monetização)
- [Onde a experiência dele (DevSecOps) entra de verdade](#onde-a-experiência-dele-devsecops-entra-de-verdade)
- [Riscos e mitigação](#riscos-e-mitigação)
- [Fases recomendadas](#fases-recomendadas)

---

## Tese central

Existe dor real e validada: pessoa física com processo arquivado/absolvido que continua aparecendo no Google, Escavador ou JusBrasil; notícia antiga com dado sensível que não some do índice de busca; presença digital que atrapalha emprego, crédito ou vida pessoal muito depois do fato original. Esse mercado já existe fora do Brasil (Incogni, DeleteMe, Optery, focados em corretores de dados nos EUA) e a demanda para o recorte brasileiro/europeu ainda não tem um player dominante e confiável.

O que decide se isso é um negócio sério ou uma promessa que não se sustenta é **até onde M3Sec pode agir sem advogado, e a partir de onde precisa de um advogado com OAB ativa assinando**. Ignorar essa linha é o maior risco estratégico do projeto — pior que qualquer risco técnico ou de concorrência.

---

## O risco de fundo: isso pode virar exercício ilegal da advocacia

Registrando aqui pra não ser reaberto depois, como o `readme.md` do Imersão faz com suas próprias decisões.

**No Brasil, não existe "direito ao esquecimento" genérico.** O STF decidiu isso no Tema 786 (RE 1010606, 2021): não há um direito amplo de apagar informação verídica e legalmente publicada só porque incomoda depois de um tempo. Remoção de resultado do Google, do Escavador ou do JusBrasil não é um botão que se aperta — depende de fundamento jurídico específico por caso: dado sensível (art. 5º, II da LGPD), processo já arquivado/absolvido cuja manutenção pública fere presunção de inocência, decisão judicial de segredo de justiça descumprida pela plataforma, dado desatualizado que induz a erro sobre a pessoa, entre outros.

**Consequência prática pro modelo de negócio:** montar e protocolar uma petição jurídica fundamentada, negociar com uma plataforma citando dispositivo legal específico, ou entrar com ação judicial — isso é ato privativo de advogado (Lei 8.906/94, art. 1º). Uma empresa de tecnologia oferecendo isso como "serviço" sem advogado assinando incorre em exercício ilegal da profissão. Isso não é um detalhe de compliance, é o que separa M3Sec de virar uma empresa com risco criminal.

**Decisão de arquitetura de negócio:** M3Sec não é um escritório de advocacia disfarçado de startup. É uma empresa de tecnologia que **monitora, documenta e opera o pipeline operacional**, e **faz parceria com advogado(s) com OAB ativa** pra qualquer ato que exija capacidade postulatória. Ver divisão de camadas abaixo.

---

## Dividir o produto por camada jurídica

Espelhando a lógica que já funcionou no Imersão (dividir por risco, não tratar como produto único):

| | Monitoramento/descoberta | Solicitação direta ao controlador (opt-out) | Petição fundamentada / ação judicial |
|---|---|---|---|
| O que é | Rastrear onde o dado da pessoa aparece: Google, Escavador, JusBrasil, corretores de dados, notícias | Pedido padrão de remoção/opt-out enviado em nome do titular, com autorização dele — mesmo modelo que Incogni/DeleteMe usam nos EUA/UE | Fundamentação jurídica específica (LGPD, sigilo, dado sensível), negociação formal ou ação judicial |
| Exige advogado? | Não | Zona cinzenta — GDPR e LGPD preveem que o titular pode agir por meio de representante pra exercer seus próprios direitos; ainda assim, o *texto* do pedido deveria ser revisado por advogado antes de padronizar | Sim, sempre |
| Quem executa | Produto/tecnologia (M3Sec) | Produto/tecnologia, com template validado por advogado parceiro | Advogado parceiro, M3Sec só instrui o caso e entrega o dossiê pronto |
| Este é o produto principal? | Sim — é a base de tudo, e sozinho já é vendável (visibilidade é valor) | Sim, esperado como a oferta central para o cliente comum | Só para os casos que a camada anterior não resolve — cobrado à parte, repassado ao parceiro jurídico |

**Recomendação:** o pitch público nunca deveria ser "nós removemos qualquer coisa sua da internet" — isso é a versão M3Sec do erro do Cluely no Imersão (prometer o que não se sustenta juridicamente gera dano reputacional maior que não vender o item). O pitch defensável é "monitoramos sua exposição de dados e cuidamos do processo de remoção — incluindo, quando necessário, com advogado parceiro".

---

## Segmentação de mercado

### Primário
- **Pessoa física com processo judicial arquivado/absolvido** ainda indexado no Google/Escavador/JusBrasil, prejudicando emprego ou crédito.
- **Profissional liberal com reputação = ativo de negócio** (médico, advogado, corretor, consultor) que sofre com notícia antiga ou avaliação difamatória bem posicionada no Google.

### Adjacentes
- Cidadão/residente na UE (ou brasileiro com dados processados por empresa europeia) exercendo direito de apagamento do GDPR contra big techs e corretores de dados.
- Vítima de exposição indevida (vazamento de dados, doxxing, revenge porn — este último já tem amparo legal mais forte no Brasil, inclusive criminal).
- Empresas pequenas/médias com sócio ou executivo cuja reputação pessoal afeta a marca.

### Não-óbvio, mas plausível
- Escritórios de advocacia pequenos como canal **B2B2C**: eles têm o cliente e a demanda, mas não têm o pipeline de monitoramento/tecnologia — M3Sec pode ser o back-office técnico deles.
- Empresas de recrutamento/RH como canal inverso: due diligence de candidato encontra informação desatualizada que devia ter sido removida — não é cliente direto, mas valida a dor do lado oposto.

---

## Panorama competitivo

- **Incogni, DeleteMe, Optery** (EUA/global): removem dados de corretores de dados (data brokers). Modelo validado, assinatura recorrente, sem estigma. Não cobrem bem o recorte brasileiro (Escavador, JusBrasil não são "data brokers" no sentido americano) nem a complexidade da jurisprudência do STF sobre direito ao esquecimento.
- **Escritórios de advocacia especializados em "reputação digital"/"direito ao esquecimento"** no Brasil: já existem, cobram caro, processo manual, pouca tecnologia. M3Sec compete oferecendo o que eles não têm — monitoramento contínuo e operação em escala — não competindo na parte jurídica em si (ali, é parceiro, não concorrente).
- **Empresas de "reputação online"/SEO reputacional**: tentam "empurrar pra baixo" conteúdo negativo no ranking em vez de removê-lo. Categoria com histórico de promessas exageradas — vale diferenciar M3Sec claramente disso no discurso público.

---

## Modelo de monetização

- **Assinatura mensal (monitoramento contínuo)** — modelo Incogni/DeleteMe: escaneamento recorrente + solicitações de opt-out incluídas. Recorrente, previsível, mas exige volume de scans automatizado (custo técnico baixo por cliente).
- **Taxa por caso (remoção pontual)** — para o item específico (aquele processo no Escavador, aquela notícia) que o cliente já sabe que quer resolver. Fecha rápido, menor LTV.
- **Repasse/parceria com advogado** — quando o caso exige petição/ação judicial, M3Sec cobra pelo dossiê+encaminhamento, o advogado cobra pelos honorários do ato jurídico. Modelo de comissão de indicação precisa respeitar o Código de Ética da OAB (vedação a captação de cliente por terceiros de forma mercantilizada) — **validar formato de parceria com o próprio advogado antes de desenhar o contrato comercial**.
- **B2B2C com escritórios pequenos** — M3Sec como fornecedor de tecnologia white-label para escritórios que já têm a carteira de clientes.

---

## Onde a experiência dele (DevSecOps) entra de verdade

Isso é o diferencial real, não genérico:

- **Monitoramento automatizado**: scraping/APIs de busca (Google, dorks estruturados), Escavador, JusBrasil, alertas de novo conteúdo indexado sobre o titular — pipeline de dados, exatamente a competência de 15 anos em automação/observabilidade.
- **Geração de templates de solicitação**: um LLM (a mesma stack já usada no Imersão — Anthropic Claude) pode gerar o rascunho do pedido de remoção citando o dispositivo legal certo, revisado e aprovado por advogado antes de virar template padrão — não gerar petição ad-hoc sem revisão humana qualificada.
- **Dashboard de caso**: status de cada solicitação (enviada, em análise, negada, escalada pro advogado, resolvida) — CRUD simples, nada exótico, mas é o que profissionaliza o serviço frente a um escritório de advocacia manual.
- **Segurança dos dados do próprio cliente**: M3Sec vai armazenar dado extremamente sensível de terceiros (processo judicial, dado de saúde, etc.) — a experiência em ISO 27001, controle de acesso e criptografia não é um "nice to have" aqui, é o que evita que M3Sec vire ela mesma um vazamento de dados sensíveis.

---

## Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Exercício ilegal da advocacia | Nunca protocolar/fundamentar petição sem advogado assinando; contrato de parceria jurídica desenhado com o próprio advogado antes de vender qualquer camada 3 |
| Prometer remoção que a jurisprudência não garante | Comunicação nunca promete "remoção garantida" — promete processo, tentativa fundamentada e transparência de resultado, igual ao que Incogni já faz (eles não garantem 100%) |
| M3Sec vira ela mesma um risco de vazamento de dado sensível | Segurança desde o dia 1 (é a competência dele) — não é opcional dado o tipo de dado armazenado |
| Captação de cliente pra advogado violando ética da OAB | Desenhar o repasse como prestação de serviço de tecnologia, não como intermediação remunerada de cliente para advogado — validar com o próprio parceiro jurídico |
| Concorrência de escritórios estabelecidos | Vantagem defensável é tecnologia/escala (monitoramento contínuo automatizado), não a parte jurídica em si |

---

## Fases recomendadas

1. **Fase 1 — Validar a dor com escopo mínimo e legal desde o início.** Um advogado parceiro definido antes de vender qualquer coisa além de monitoramento puro. Monitoramento (camada 1) como produto standalone: "descubra onde seus dados aparecem" — zero risco jurídico, já é vendável sozinho.
2. **Fase 2 — Solicitação direta/opt-out (camada 2)** com templates validados pelo parceiro jurídico, para os casos que não exigem ação judicial.
3. **Fase 3 — Parceria formalizada para camada 3** (petição/ação judicial), com contrato de repasse claro e dentro das regras da OAB.

---

**Versão:** 0.1 — rascunho inicial, setembro/2026.
