# Auditoria Final da Entrega Arquitetural

## 1. Resumo executivo

**Conclusão:** A entrega não satisfaz integralmente os quatro prompts.

Os artefatos documentam bem as fontes, as três personas oficiais, os requisitos RF-01 a RF-23 e RNF-01 a RNF-18, as regras RN-01 a RN-10 e a restrição CON-01. `docs/arquitetura.md` também contém C4 em Mermaid, sequências, utility tree, cenários ATAM, trade-offs, riscos, painel multidisciplinar, ADRs inline e matriz de rastreabilidade.

Entretanto, a entrega é predominantemente uma baseline conceitual. O próprio documento informa que as evidências não foram executadas, que mecanismos essenciais permanecem pendentes e que várias métricas são hipóteses. Os critérios de auditoria exigem comprovação verificável, cenários mínimos explícitos, táticas de Len Bass e rastreabilidade ponta a ponta; esses pontos não estão completos.

## 2. Artefatos consultados

- [docs/prd.md](docs/prd.md): personas de origem, RF-01 a RF-23, RNF-01 a RNF-18, RN-01 a RN-10, escopos, dependências e evidências esperadas.
- [docs/fluxos-personas.md](docs/fluxos-personas.md): fontes, jornadas, FLX-01 em diante, ciclo de vida, autorizações, exceções e pendências.
- [docs/personas/solicitante.md](docs/personas/solicitante.md).
- [docs/personas/responsavel.md](docs/personas/responsavel.md).
- [docs/personas/administrador.md](docs/personas/administrador.md).
- [docs/arquitetura.md](docs/arquitetura.md): baseline arquitetural, C4, sequências, ATAM, ADRs e matriz.
- [docs/relatorio-validacao-arquitetura.md](docs/relatorio-validacao-arquitetura.md): validação documental anterior.
- [README.md](README.md): identificação do projeto; não acrescenta requisitos de domínio.

Não foram encontrados documentos separados de ADR, diagramas, matrizes ou decisões anteriores. As decisões arquiteturais estão dentro de `docs/arquitetura.md`, seções 17 e 37.

## 3. Resultado do Prompt 1: descoberta e drivers

**PARCIAL.** As fontes foram identificadas e os identificadores foram preservados. Há separação explícita de fatos, lacunas, tensões e suposições em [docs/arquitetura.md](docs/arquitetura.md#L186) e de fontes e pendências em [docs/fluxos-personas.md](docs/fluxos-personas.md#L45). CON-01 foi corretamente marcado como restrição adicional do exercício em [docs/arquitetura.md](docs/arquitetura.md#L88).

O resultado não é completo porque a matriz de drivers, em [docs/arquitetura.md](docs/arquitetura.md#L152), registra prioridade e origem, mas não justifica individualmente cada prioridade nem demonstra a presença de cada driver em uma decisão aceita. Vários drivers são necessidades ou candidatos, não decisões aprovadas. As decisões de domínio anteriores não existem como fonte separada; portanto, a leitura integral dessa categoria não pode ser comprovada.

**Conforme:** fontes oficiais localizadas; três personas preservadas; RF/RNF/RN preservados; fatos, lacunas, tensões e suposições explicitados.

**Parcial:** prioridades sem justificativa individual; decisões anteriores ausentes como artefato; drivers batch sem requisito de produto correspondente, embora isso seja marcado.

**Ausente:** evidência de que qualquer driver tenha sido validado fora da documentação.

## 4. Resultado do Prompt 2: arquitetura C4 e pipeline diário

**PARCIAL.** Existem diagramas C4 de contexto, contêineres e componentes em [docs/arquitetura.md](docs/arquitetura.md#L310), e o online está separado conceitualmente do batch em [docs/arquitetura.md](docs/arquitetura.md#L271). O cron diário ao final do dia, o treino/retreino e os dados novos aparecem como CON-01.

Faltam decisões e evidências para o mecanismo de concorrência, checkpoint, idempotência, lock, retry, timeout, recuperação, promoção, rollback, modelo ativo e impacto de recursos. A sequência batch representa capacidades, mas deixa o avanço do checkpoint e a política de promoção como futuras. A separação online/batch é candidata, não uma garantia comprovada.

## 5. Resultado do Prompt 3: análise ATAM

**PARCIAL.** A utility tree e 18 cenários estão em [docs/arquitetura.md](docs/arquitetura.md#L608) e [docs/arquitetura.md](docs/arquitetura.md#L631). Há sensibilidades, trade-offs, riscos, não-riscos e temas de risco em [docs/arquitetura.md](docs/arquitetura.md#L887), [docs/arquitetura.md](docs/arquitetura.md#L900) e [docs/arquitetura.md](docs/arquitetura.md#L927).

Os cenários possuem a estrutura textual das seis partes, mas vários não possuem métrica aprovada: as métricas de ATAM-06 a ATAM-12, ATAM-15, ATAM-16 e ATAM-18 são explicitamente hipóteses pendentes. A cobertura mínima solicitada não está completa: não há cenários explícitos e independentes para reexecução, dados duplicados, alteração de esquema, promoção incompleta, indisponibilidade do registry, custo acima da janela, tempo acima da janela e impacto do batch no online. A arquitetura reconhece alguns desses temas em texto, mas isso não substitui um cenário ATAM verificável.

Também falta a tática arquitetural de Len Bass para cada decisão/cenário. Não há seção ou campo de tática de Len Bass nos artefatos consultados.

## 6. Resultado do Prompt 4: revisão cruzada, ADRs e rastreabilidade

**PARCIAL.** A revisão dos seis papéis possui objeções reais e recomendações fundamentadas em [docs/arquitetura.md](docs/arquitetura.md#L1048), incluindo divergências consolidadas em [docs/arquitetura.md](docs/arquitetura.md#L1139). Há 14 ADRs inline em [docs/arquitetura.md](docs/arquitetura.md#L1231), e uma matriz requisito → decisão → componente → evidência em [docs/arquitetura.md](docs/arquitetura.md#L1429).

O resultado não é completo porque as colunas da matriz são evidências esperadas, não evidências encontradas; vários registros classificam a cobertura como “coberta” mesmo com mecanismo ou aprovação pendentes; decisões de domínio relevantes não têm ADR próprio; e os ADRs não têm campo explícito para tática de Len Bass. A própria seção 25 do relatório anterior confirma que não houve execução de build, testes, C4 renderizado, batch, treinamento, promoção ou rollback em [docs/relatorio-validacao-arquitetura.md](docs/relatorio-validacao-arquitetura.md#L766).

## 7. Itens conformes

- As três personas oficiais são as únicas personas de produto: [docs/arquitetura.md](docs/arquitetura.md#L70).
- RF-01 a RF-23, RNF-01 a RNF-18 e RN-01 a RN-10 são identificados e preservados: [docs/prd.md](docs/prd.md#L123), [docs/prd.md](docs/prd.md#L205), [docs/prd.md](docs/prd.md#L1014).
- CON-01 é distinguida da baseline e sua origem é indicada como restrição adicional: [docs/arquitetura.md](docs/arquitetura.md#L88).
- Há separação conceitual entre online e batch: [docs/arquitetura.md](docs/arquitetura.md#L271).
- Há diagramas Mermaid para contexto, contêineres e componentes: [docs/arquitetura.md](docs/arquitetura.md#L310).
- Há pelo menos um trade-off explicitamente nomeado: TO-01 em [docs/arquitetura.md](docs/arquitetura.md#L900).
- A revisão cruzada contém objeções, riscos, perguntas e recomendações diferentes por papel: [docs/arquitetura.md](docs/arquitetura.md#L1055).
- Nenhum risco alto ou crítico foi declarado aceito: [docs/arquitetura.md](docs/arquitetura.md#L1548).
- A documentação declara que evidência esperada não equivale a evidência executada: [docs/arquitetura.md](docs/arquitetura.md#L16).

## 8. Itens parciais

| Item | O que existe | O que falta | Evidência | Correção necessária |
|---|---|---|---|---|
| Drivers | Origem, prioridade e síntese | Justificativa individual e decisão aceita | [arquitetura.md](docs/arquitetura.md#L152) | Vincular cada driver a decisão, cenário, componente e evidência real. |
| CON-01 | Cron, final do dia, treino/retreino e dados novos | Semântica de dados novos e mecanismo operacional | [arquitetura.md](docs/arquitetura.md#L108) | Registrar origem, decisão e experimento sem inventar finalidade. |
| C4 | Três níveis Mermaid | Verificação renderizada e correspondência completa | [arquitetura.md](docs/arquitetura.md#L310) | Validar nomes, relações e níveis contra o texto. |
| Batch | Etapas conceituais | Controle efetivo, falha, recuperação e promoção | [arquitetura.md](docs/arquitetura.md#L382) | Completar decisões ou manter explicitamente bloqueado. |
| Utility tree | Atributo, refinamento, cenário, importância e dificuldade | Justificativa verificável de importância/dificuldade | [arquitetura.md](docs/arquitetura.md#L608) | Adicionar fundamento e rastreabilidade por entrada. |
| Cenários | Seis campos textuais em cada ATAM | Métricas aprovadas e evidência | [arquitetura.md](docs/arquitetura.md#L631) | Classificar como FRACO enquanto métrica/decisão/evidência faltarem. |
| ADRs | 14 registros inline com alternativas e consequências | Tática Len Bass, evidência executada e ADRs de domínio | [arquitetura.md](docs/arquitetura.md#L1231) | Completar campos e registrar decisões relevantes ausentes. |
| Matriz | Relação requisito → decisão → componente → evidência esperada | Evidência localizada e cobertura de todos os vínculos | [arquitetura.md](docs/arquitetura.md#L1429) | Trocar expectativa por referência verificável ou marcar ausente. |
| Revisão cruzada | Objeções reais por seis papéis | Resolução formal das divergências | [arquitetura.md](docs/arquitetura.md#L1139) | Registrar decisão, responsável e evidência de resolução. |

## 9. Itens ausentes

| Requisito da atividade | Onde deveria aparecer | Impacto | Correção necessária |
|---|---|---|---|
| Tática de Len Bass por decisão/cenário | ADRs, ATAM e matriz | Não permite avaliar intenção arquitetural | Associar tática existente do catálogo, sem inventar solução. |
| Cenário explícito de reexecução | Utility tree e cenários ATAM | Idempotência não é pressionada isoladamente | Criar cenário somente com origem CON-01 e métrica a validar. |
| Cenários de duplicação, esquema e registry indisponível | Utility tree e cenários ATAM | Falhas críticas do batch não são verificáveis | Registrar como ausentes e detalhar apenas após definição. |
| Promoção incompleta e impacto do batch no online | Cenários, sequência e matriz | As invariantes não são comprováveis | Modelar resposta e evidência, mantendo bloqueios atuais. |
| ADR separado para decisões de domínio | ADRs | Estado e ocupação de `SOLICITADA` permanecem sem decisão rastreável | Registrar decisão somente após aprovação da equipe. |
| Evidências executadas | Matriz e relatório | Não comprova RNF, invariantes ou decisões | Anexar resultados reais; não tratar “evidência esperada” como prova. |

## 10. Inconsistências

- [docs/relatorio-validacao-arquitetura.md](docs/relatorio-validacao-arquitetura.md#L405) afirma que a utility tree cobre integralmente os estímulos exigidos, mas não existem cenários explícitos para vários itens mínimos: reexecução, dados duplicados, alteração de esquema, promoção incompleta, registry indisponível, custo/tempo acima da janela e impacto do batch no online.
- [docs/arquitetura.md](docs/arquitetura.md#L1188) classifica falha parcial, jobs sobrepostos, candidato pior e rollback como “COBERTA”, enquanto a mesma tabela informa política, métricas, procedimento ou tempo-alvo pendentes.
- [docs/arquitetura.md](docs/arquitetura.md#L434) envia atualização de progresso após a validação, mas não define atomicidade nem o ponto de sucesso; a seção 15.2 também registra “política futura”.
- [docs/arquitetura.md](docs/arquitetura.md#L324) apresenta “Notificação ou API externa” no C4, enquanto RF-20 ainda não escolheu a alternativa; é aceitável como candidato, mas não como integração arquitetural confirmada.
- [docs/arquitetura.md](docs/arquitetura.md#L239) recomenda monólito modular e [docs/arquitetura.md](docs/arquitetura.md#L1233) registra ADR-001, mas ambos mantêm o status proposto/candidato; qualquer texto que trate essa estrutura como decisão definitiva seria inconsistente.
- [docs/arquitetura.md](docs/arquitetura.md#L377) usa “Aplica decisão aprovada” no componente de estados, embora a própria seção 12 deixe as transições e o estado inicial pendentes.
- A matriz registra “COBERTA” ou “COBERTA DOCUMENTALMENTE” para itens cuja evidência é explicitamente não executada em [docs/arquitetura.md](docs/arquitetura.md#L1447). Isso conflita com o critério de auditoria que exige evidência verificável.

## 11. Suposições que podem ter virado fatos

Não há evidência de que as suposições abaixo tenham sido declaradas como requisitos, mas elas aparecem como abordagens operacionais e devem continuar marcadas como hipóteses:

- `SUP-01`: monólito modular suficiente para a escala inicial.
- `SUP-02`: batch fora do caminho online.
- `SUP-03`: fonte permite identificação incremental.
- `SUP-04`: versão anterior pode ser preservada.
- `SUP-05`: dados podem ser minimizados sem invalidar o treino.
- `SUP-06`: equipe consegue operar sinais mínimos.

Origem e tratamento: [docs/arquitetura.md](docs/arquitetura.md#L1489). O risco de conversão indevida permanece porque C4, sequência e recomendações já dependem dessas abordagens.

## 12. Números e métricas sem origem

Os números oficiais possuem origem no PRD: cobertura de linhas 80%, branches 70%, 100% de rastreabilidade, zero bugs críticos e zero vulnerabilidades críticas em [docs/prd.md](docs/prd.md#L1014). Os demais valores abaixo estão marcados como hipótese ou pendência, portanto não são fatos, mas ainda não são métricas aprovadas:

- “exatamente 1 aceita e 0 conflitos persistidos” em ATAM-01;
- “0 omissões”, “0 duplicações”, “uma execução efetiva” e “0 antigos classificados como novos” nos cenários batch;
- carga, percentis, erro, duração e tempo de rollback;
- tolerância de atraso, quantidade de retries, thresholds de qualidade e métricas de modelo.

Localização: [docs/arquitetura.md](docs/arquitetura.md#L705) e [docs/arquitetura.md](docs/arquitetura.md#L718). Classificação: **PARCIAL**, pois a rotulagem como hipótese existe, mas a validação pendente não foi resolvida.

## 13. Tecnologias sem justificativa

As tecnologias com origem explícita no produto são Java 21, Spring Boot 3.x, JUnit 5, Testcontainers, WireMock, GitHub Actions, JaCoCo, SonarCloud e JMeter: [docs/prd.md](docs/prd.md#L1014). Não foram encontradas tecnologias batch/ML, registry, scheduler, banco específico, cache, réplica ou infraestrutura dedicada aprovadas.

O monólito modular, persistência relacional, armazenamento de artefatos e observabilidade aparecem como propostas ou contêineres conceituais, não como escolhas aprovadas. Classificação: **PARCIAL** para a atividade, porque a rastreabilidade da justificativa ainda não contém tática, evidência ou experimento concluído.

## 14. Cenários ATAM incompletos

Todos os 18 cenários têm campos textuais de fonte, estímulo, ambiente, artefato, resposta e métrica. Contudo, são **FRACOS** quando a métrica é hipótese, a decisão está pendente ou não há evidência. Isso afeta ATAM-06, ATAM-07, ATAM-08, ATAM-09, ATAM-10, ATAM-11, ATAM-12, ATAM-15, ATAM-16 e ATAM-18: [docs/arquitetura.md](docs/arquitetura.md#L699).

Também estão ausentes como cenários mínimos independentes: reexecução; dados duplicados; alteração de esquema; promoção incompleta; indisponibilidade do registry; custo acima da janela; tempo acima da janela; e impacto do batch no online. O cenário ATAM-14 cobre vazamento, mas uso indevido de dados não é separado como cenário verificável.

Não há cenários “sem fonte” ou “sem origem” no conjunto existente. Há cenários sem métrica aprovada, sem decisão definitiva, sem tática de Len Bass e sem evidência executada.

## 15. Decisões sem tática ou evidência

| Decisão | Tática | Cenário | Métrica | Evidência |
|---|---|---|---|---|
| ADR-002, concorrência | Ausente | ATAM-01/02/15 | Parcial/hipótese | Não executada |
| ADR-004, estado-auditoria | Ausente | ATAM-04 | Definida como zero, sem execução | Não executada |
| ADR-007/008, incrementalidade e jobs | Ausente | ATAM-07/08/09/18 | Hipóteses | Não executada |
| ADR-009, retry | Ausente | ATAM-08/13 | Sem timeout/taxonomia aprovada | Não executada |
| ADR-011, gates/promoção/rollback | Ausente | ATAM-11/12 | Bloqueada pela finalidade | Não executada |
| ADR-012/013/014, observabilidade, LGPD e custos | Ausente | ATAM-06/10/14/15 | Pendentes | Não executada |
| Estado inicial, transições e ocupação de `SOLICITADA` | Ausente | ATAM-01/05/16 | Não definida | Não localizada |

## 16. ADRs incompletos ou ausentes

Os ADRs-001 a 014 possuem contexto, forças, alternativas, decisão/condição, consequências, riscos, requisitos, cenários e evidência esperada em [docs/arquitetura.md](docs/arquitetura.md#L1231). Portanto, a estrutura documental é **PARCIALMENTE CONFORME**.

Pendências comuns: não há tática de Len Bass; não há evidência executada; não há condição operacional comprovada de revisão; e alguns ADRs registram necessidades, não decisões. Estão sem ADR próprio ou sem registro decisório concluído: estado inicial e ocupação de `SOLICITADA`, transições e atores, critério de recurso restrito, bloqueio versus manutenção, reservas existentes afetadas, fórmula dos relatórios e escolha de RF-20.

## 17. Cobertura da matriz de rastreabilidade

**Requisitos cobertos documentalmente:** RF-01 a RF-23, RN-01 a RN-10 e RNF-01 a RNF-18 aparecem em linhas agrupadas na matriz de [docs/arquitetura.md](docs/arquitetura.md#L1429).

**Parcialmente cobertos:** RN-04/RNF-09, RN-05, RN-07, RN-09, RF-20, RF-21, RF-22, RNF-02, RNF-03, RNF-05 a RNF-14, RNF-16 e CON-01, por mecanismo, escolha, fórmula, meta ou execução pendentes.

**Sem cobertura definitiva:** estado inicial e transições; critério de recurso restrito; bloqueio versus manutenção; reservas existentes afetadas; finalidade e uso de CON-01; métricas de ML; LGPD; metas JMeter; critérios de acessibilidade.

**Decisões sem requisito correspondente:** separação lógica/física do batch, checkpoint específico, exclusão de jobs, registry, promoção/rollback, observabilidade, papel técnico do modelo, cache e infraestrutura dedicada. O documento os lista explicitamente em [docs/arquitetura.md](docs/arquitetura.md#L1474), mas isso não elimina a ausência de requisito.

**Evidências ausentes:** todas as evidências executáveis listadas como “EVIDÊNCIA NÃO EXECUTADA” em [docs/arquitetura.md](docs/arquitetura.md#L1448).

## 18. Riscos e temas de risco

**Riscos confirmados/documentados:** RA-01 a RA-16 em [docs/arquitetura.md](docs/arquitetura.md#L927), incluindo concorrência, auditoria, autorização, incrementalidade, jobs sobrepostos, candidato pior, rollback, LGPD, falha externa e complexidade prematura.

**Dúvidas ainda não investigadas:** finalidade de CON-01, semântica de dados novos, dataset, algoritmo, métricas, base legal, mecanismo de checkpoint, retry, lock, promoção, rollback e custos.

**Riscos aceitos:** nenhum risco alto ou crítico foi aceito. Não é possível informar quem aceitou cada risco porque não existe aceitação registrada: [docs/arquitetura.md](docs/arquitetura.md#L1548).

**Riscos residuais:** permanecem todos os riscos bloqueantes de domínio, batch, segurança, operação e evidência listados em [docs/arquitetura.md](docs/arquitetura.md#L1209).

**Temas de risco:** integridade transacional; segurança contextual; governança de CON-01; operação e recuperação; complexidade prematura: [docs/arquitetura.md](docs/arquitetura.md#L955).

## 19. Correções obrigatórias

| Prioridade | Artefato | Relação | Alteração necessária | Evidência esperada |
|---|---|---|---|---|
| Alta/Alta, já registrada | `docs/arquitetura.md` | ATAM-01, RN-04 | Completar cenário e experimento de concorrência, sem escolher mecanismo por preferência | Teste concorrente em banco realista |
| Alta/Alta, já registrada | `docs/arquitetura.md` | ATAM-04, RN-09 | Definir e testar limite de consistência estado-auditoria | Injeção de falha e resultado |
| Alta/Alta, já registrada | `docs/arquitetura.md` | ATAM-07/08/09/18, CON-01 | Separar reexecução, duplicação, esquema, dados tardios e checkpoint em cenários verificáveis | Casos de omissão/duplicação e progresso |
| Alta/Alta, já registrada | `docs/arquitetura.md` | ATAM-10/11/12/14, CON-01 | Completar qualidade, candidato pior, promoção incompleta, registry, rollback, vazamento e uso indevido | Testes e inventário aprovados |
| Alta/Média ou Alta/Alta | `docs/arquitetura.md` | ATAM batch | Acrescentar cenários explícitos de custo/tempo acima da janela e impacto online | Medição aprovada; valores continuam pendentes até decisão |
| Transversal | `docs/arquitetura.md` | Todos os ADRs/ATAM | Associar tática de Len Bass, atributo, cenário, métrica e evidência | Referência verificável do catálogo e teste/experimento |
| Transversal | `docs/arquitetura.md` | Matriz | Diferenciar cobertura documental de evidência executada e localizar cada prova | Link/artefato de resultado real |
| Bloqueante | Fontes e arquitetura | Estado e CON-01 | Obter decisões humanas já apontadas, preservando alternativas e histórico | Decisão aprovada ou pendência formal, sem inventar requisito |

## 20. Checklist final

| Área auditada | Status |
|---|---|
| Fontes e personas | CONFORME |
| Requisitos e regras preservados | CONFORME |
| Fatos, lacunas, conflitos e suposições | PARCIAL |
| Drivers rastreáveis e justificados | PARCIAL |
| Restrição CON-01 explicitada | CONFORME |
| Cron diário ao final do dia | CONFORME documentalmente; evidência AUSENTE |
| Treino/retreino somente com dados novos | PARCIAL |
| C4 contexto, contêineres e componentes | PARCIAL |
| Separação online/batch | PARCIAL |
| Sequência online | PARCIAL |
| Sequência batch | PARCIAL |
| Invariante batch não compromete online | AUSENTE como prova |
| Invariante checkpoint só avança após sucesso | PARCIAL |
| Invariante candidato pior não é promovido | PARCIAL |
| Controles batch 1-25 | PARCIAL; vários pendentes ou ausentes |
| Observabilidade | PARCIAL |
| Segurança e LGPD | PARCIAL |
| Custos/FinOps | PARCIAL |
| Utility tree | PARCIAL |
| Cenários com seis partes | PARCIAL |
| Cobertura mínima de cenários ATAM | AUSENTE |
| Sensibilidades | CONFORME documentalmente |
| Trade-offs | CONFORME documentalmente |
| Riscos, não-riscos e temas | PARCIAL |
| Revisão dos seis papéis | CONFORME documentalmente |
| Táticas de Len Bass | AUSENTE |
| ADRs para decisões relevantes | PARCIAL |
| Matriz requisito → decisão → componente → evidência | PARCIAL |
| Riscos aceitos com responsável | AUSENTE; nenhum aceito |
| Próximos experimentos | CONFORME como lista, não executados |
| Evidências executadas | AUSENTE |

## 21. Conclusão

A entrega não satisfaz integralmente os quatro prompts.

As fontes, identificadores, personas, requisitos, restrição CON-01, diagramas, ATAM, objeções do painel, trade-offs, riscos, ADRs inline e matriz estão documentados. Porém, os artefatos também comprovam que os mecanismos críticos permanecem pendentes, que várias métricas são hipóteses, que não existem evidências executadas, que faltam táticas de Len Bass e que parte da cobertura mínima de cenários ATAM não foi modelada explicitamente.

### PENDÊNCIAS QUE IMPEDEM O FECHAMENTO

- Executar e registrar evidências para as invariantes e RNFs, não apenas evidências esperadas.
- Completar os cenários ATAM mínimos ausentes e suas métricas, mantendo hipóteses como validação pendente.
- Associar táticas de Len Bass às decisões e cenários.
- Resolver, ou manter formalmente bloqueadas com rastreabilidade, as decisões de domínio, concorrência, incrementalidade, recuperação, promoção, LGPD e custo.
- Corrigir a classificação de cobertura que confunde presença documental com comprovação verificável.