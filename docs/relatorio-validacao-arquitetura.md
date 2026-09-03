# Relatório de Validação da Arquitetura

> **Documento avaliado:** `docs/arquitetura.md`  
> **Produto:** Organização de Recursos  
> **Natureza da avaliação:** revisão documental de arquitetura, avaliação ATAM e painel multidisciplinar  
> **Status:** concluído documentalmente, com decisões, riscos e evidências pendentes registrados  
> **Data:** 2026-09-02  
> **Resultado geral:** arquitetura consistente e adequada para deliberação, experimentação e evolução controlada

## 1. Objetivo

Este relatório consolida a validação documental da arquitetura do sistema Organização de Recursos. A revisão verifica a aderência do documento arquitetural às fontes oficiais, a cobertura dos requisitos e drivers, a qualidade das decisões propostas, a consistência entre as visões arquiteturais e a suficiência da avaliação de riscos.

A validação contempla:

- requisitos funcionais, não funcionais e regras de negócio;
- personas, autorizações e limites operacionais;
- drivers e atributos de qualidade;
- responsabilidades, limites e interfaces;
- arquitetura do núcleo online;
- processamento batch associado a CON-01;
- diagramas C4 e sequências críticas;
- utility tree e cenários ATAM;
- pontos de sensibilidade e trade-offs;
- riscos, não-riscos e temas de risco;
- pareceres do painel multidisciplinar;
- divergências arquiteturais;
- registros de decisão arquitetural;
- rastreabilidade entre requisito, decisão, componente e evidência;
- lacunas, suposições, perguntas abertas, riscos aceitos e experimentos recomendados.

A revisão não modifica as fontes do produto, não transforma hipótese em fato e não considera uma alternativa aprovada sem status explícito.

## 2. Fontes e hierarquia documental

### 2.1 Fontes consideradas

- `docs/prd.md`;
- `docs/fluxos-personas.md`;
- `docs/personas/solicitante.md`;
- `docs/personas/responsavel.md`;
- `docs/personas/administrador.md`;
- `docs/arquitetura.md`;
- CON-01, restrição adicional do exercício arquitetural.

### 2.2 Hierarquia adotada

1. O PRD, os fluxos e as personas definem o produto.
2. `docs/arquitetura.md` interpreta os impactos arquiteturais sem alterar os requisitos.
3. CON-01 permanece identificada como restrição adicional, separada da baseline original.
4. Decisões pendentes, candidatas ou bloqueadas não são tratadas como requisitos.
5. Evidências esperadas não são tratadas como evidências executadas.

### 2.3 Convenções de status

| Status | Interpretação |
|---|---|
| APROVADO NA BASELINE | Exigido por requisito ou regra de negócio oficial |
| PROPOSTO | Recomendação arquitetural ainda sujeita à deliberação |
| PENDENTE DE DECISÃO | Exige definição humana antes da solução definitiva |
| PENDENTE DE EXPERIMENTO | Exige evidência técnica antes da escolha |
| BLOQUEADO | Não deve avançar enquanto uma condição anterior não for resolvida |
| HIPÓTESE PENDENTE | Valor ou comportamento proposto, sem aprovação como meta |
| EVIDÊNCIA NÃO EXECUTADA | Validação prevista, mas ainda sem resultado real registrado |

## 3. Escopo da validação

A avaliação abrangeu:

1. contexto, objetivo, escopo e limites;
2. personas oficiais e responsabilidades;
3. requisitos arquiteturalmente significativos;
4. atributos de qualidade;
5. drivers priorizados;
6. riscos iniciais;
7. arquitetura lógica e modularidade;
8. responsabilidades, limites e interfaces;
9. diagramas de contexto, contêineres e componentes;
10. sequência online de reservas;
11. sequência batch;
12. execução diária de CON-01;
13. identificação e processamento de dados novos;
14. watermark e checkpoint;
15. idempotência;
16. coordenação de jobs sobrepostos;
17. retry e recuperação;
18. qualidade e linhagem de dados;
19. reprodutibilidade;
20. validação de candidato;
21. gates;
22. versionamento e registry;
23. promoção e rollback;
24. observabilidade;
25. segurança e LGPD;
26. custos;
27. utility tree;
28. cenários de atributos de qualidade;
29. sensibilidades e trade-offs;
30. riscos, não-riscos e temas;
31. pareceres multidisciplinares;
32. divergências e sua consolidação;
33. ADRs;
34. rastreabilidade final;
35. requisitos sem cobertura definitiva;
36. decisões sem requisito;
37. suposições e perguntas abertas;
38. riscos aceitos;
39. próximos experimentos.

## 4. Resultado executivo

A revisão concluiu que `docs/arquitetura.md` apresenta cobertura arquitetural abrangente e coerente com as informações disponíveis.

O documento avaliado:

- preserva as fontes oficiais;
- utiliza somente Solicitante, Responsável e Administrador como personas do produto;
- diferencia professor-usuário de professor-recurso;
- mantém decisões de negócio não especificadas como pendências;
- identifica os principais drivers e atributos de qualidade;
- separa o núcleo online do processamento batch em nível conceitual;
- modela CON-01 sem inventar propósito, algoritmo, dados ou métricas;
- apresenta diagramas e sequências compatíveis com as responsabilidades descritas;
- estrutura uma utility tree priorizada;
- cobre os cenários críticos do domínio, da segurança e do batch;
- registra sensibilidades, trade-offs, riscos, não-riscos e temas de risco;
- apresenta objeções fundamentadas por diferentes perspectivas;
- preserva divergências sem ocultá-las;
- registra decisões por ADR;
- relaciona requisitos, decisões, componentes e evidências;
- identifica claramente o que permanece bloqueado, pendente ou sujeito a experimento;
- não declara implementação ou execução inexistente.

### 4.1 Parecer geral

**Parecer:** favorável com condicionantes.

A arquitetura está adequada para orientar implementação e experimentação, desde que as decisões bloqueantes sejam resolvidas antes de serem tratadas como contratos definitivos.

### 4.2 Condicionantes principais

- decidir o estado inicial e a ocupação da reserva não restrita;
- selecionar e comprovar o mecanismo de concorrência de RN-04;
- definir a consistência entre mudança de estado e auditoria;
- esclarecer o propósito, os dados e o uso de CON-01;
- concluir a análise LGPD antes do uso de dados reais;
- aprovar métricas antes de gates, promoção ou rollback;
- definir metas de carga e acessibilidade antes das respectivas aprovações.

## 5. Validação das personas e autorizações

### 5.1 Personas oficiais

A arquitetura mantém exclusivamente:

- Solicitante;
- Responsável;
- Administrador.

Papéis técnicos de dados, ML, operações, segurança, custos ou avaliação não são tratados como personas do produto.

### 5.2 Limites confirmados

- O Solicitante opera somente as próprias reservas.
- Somente o Responsável autorizado aprova recursos restritos.
- O Responsável não substitui o Administrador.
- O Administrador não contorna aprovação, concorrência, estados ou auditoria.
- A autorização deve ocorrer no back-end.
- A autorização contextual deve considerar perfil, operação, propriedade e responsabilidade.

### 5.3 Professor como usuário e recurso

A diferenciação foi preservada:

- professor-usuário pode atuar como Solicitante;
- professor-recurso participa da agenda e da verificação de sobreposição;
- a relação cadastral entre as duas representações permanece pendente.

### 5.4 Resultado

**Resultado:** coerente, com pendência no modelo de identidade entre conta e recurso professor.

## 6. Validação das regras críticas

### 6.1 Concorrência

RN-04 foi corretamente interpretada como requisito de resultado:

> Duas solicitações simultâneas para o mesmo recurso e período devem produzir exatamente uma reserva aceita.

A arquitetura não transforma um mecanismo específico em exigência oficial.

Alternativas registradas:

- constraint no banco;
- isolamento transacional;
- lock pessimista;
- controle otimista;
- estrutura de slots;
- combinação de mecanismos;
- outra técnica capaz de demonstrar o comportamento exigido.

**Resultado:** requisito coberto; mecanismo pendente de experimento.

### 6.2 Sobreposição e disponibilidade

A arquitetura considera:

- sala;
- material ou equipamento;
- professor e respectiva agenda;
- manutenção;
- bloqueio, conforme definição operacional pendente;
- revalidação no momento da confirmação.

**Resultado:** cobertura coerente; tratamento de reservas existentes afetadas por nova indisponibilidade permanece pendente.

### 6.3 Estados

Estados oficiais preservados:

- `SOLICITADA`;
- `APROVADA`;
- `EM_USO`;
- `CONCLUIDA`;
- `REJEITADA`;
- `CANCELADA`;
- `NAO_COMPARECEU`.

Permanecem pendentes:

- estado inicial da reserva não restrita;
- ocupação causada por `SOLICITADA`;
- atores e condições de transições não especificadas;
- liberação de recursos;
- relação entre movimentação e conclusão.

### 6.4 RN-08

RN-08 permanece limitada à proibição de apagar reservas iniciadas. Não foi utilizada como justificativa para imutabilidade de modelos, registry, versionamento, promoção ou rollback.

### 6.5 RN-09

RN-09 permanece limitada à auditoria das mudanças de estado da reserva. A auditoria de eventos técnicos do batch é uma decisão arquitetural candidata, não uma obrigação derivada de RN-09.

### 6.6 RN-10

RN-10 sustenta a rastreabilidade dos requisitos críticos. Não torna obrigatórios Parquet, seed fixa, registry, hash, metadados específicos ou outra tecnologia de ML.

## 7. Validação dos requisitos não funcionais

| Requisito | Interpretação validada | Estado |
|---|---|---|
| RNF-01 | Java 21 e Spring Boot 3.x | Coberto |
| RNF-02 | Cobertura de linhas mínima de 80% | Estratégia coberta; evidência pendente |
| RNF-03 | Cobertura de branches mínima de 70% | Estratégia coberta; evidência pendente |
| RNF-04 | 100% dos requisitos críticos rastreados | Cobertura documental presente |
| RNF-05 | Zero bugs críticos conhecidos | Evidência pendente |
| RNF-06 | Zero vulnerabilidades críticas conhecidas | Evidência pendente |
| RNF-07 | Persistência crítica com banco containerizado | Estratégia coberta; não exige réplica |
| RNF-08 | Integração externa validada com WireMock | Aplicável após escolha de RF-20 |
| RNF-09 | Teste automatizado de concorrência | Estratégia coberta; execução pendente |
| RNF-10 | Testes em camadas | Estratégia coberta |
| RNF-11 | TDD ou BDD em funcionalidade nova | Evidência pendente |
| RNF-12 | GitHub Actions em pull requests | Estratégia coberta; execução pendente |
| RNF-13 | SonarCloud | Estratégia coberta; resultado pendente |
| RNF-14 | Medição com JMeter | Coberto; metas pendentes |
| RNF-15 | Segurança de autenticação, autorização, entrada e erros | Coberto arquiteturalmente |
| RNF-16 | Responsividade e acessibilidade | Coberto; critérios pendentes |
| RNF-17 | Erros compreensíveis e seguros | Coberto arquiteturalmente |
| RNF-18 | Documentação verificável | Coberto como estratégia |

## 8. Validação de CON-01

### 8.1 Fatos confirmados

CON-01 confirma somente:

1. execução diária;
2. execução ao final do dia;
3. treinamento ou retreinamento;
4. uso somente de dados novos.

### 8.2 Elementos não presumidos

A arquitetura não trata como fato:

- finalidade do modelo;
- problema de negócio;
- target;
- algoritmo;
- features;
- volume;
- dataset acumulado ou puramente incremental;
- tecnologia de agendamento;
- read replica;
- feature store;
- registry especializado;
- integração online;
- exactly-once;
- determinismo binário;
- hash estável;
- threshold padrão;
- promoção automática;
- rollback automático;
- quantidade de retries;
- duração máxima;
- retenção de dados e artefatos.

### 8.3 Preocupações confirmadas

| Preocupação | Tratamento arquitetural | Estado |
|---|---|---|
| Watermark/checkpoint | Alternativas para identificar dados novos e registrar progresso | Pendente de experimento |
| Idempotência | Evitar efeitos duplicados em reexecução | Pendente de mecanismo |
| Lock/coordenação | Impedir jobs incompatíveis sobrepostos | Pendente de mecanismo |
| Retry/recuperação | Classificar falhas e definir retomada sem avanço indevido | Pendente |
| Qualidade de dados | Impedir uso silencioso de dados inadequados | Critérios bloqueados pelo dataset |
| Linhagem | Relacionar fonte, execução, configuração e artefato | Campos pendentes |
| Reprodutibilidade | Preservar informações suficientes para explicar a execução | Política pendente |
| Validação | Avaliar candidato antes de qualquer uso | Métricas bloqueadas pela finalidade |
| Gates | Impedir promoção de candidato inadequado | Bloqueados |
| Registry/versionamento | Distinguir versões, se a governança exigir | Alternativa pendente |
| Promoção/rollback | Controlar entrada e retorno de versão, se houver consumo | Bloqueados |
| Observabilidade | Tornar início, etapa, volume, resultado e falha observáveis | Sinais e ferramentas pendentes |
| LGPD | Definir finalidade, base legal, minimização, acesso e retenção | Bloqueado antes de dados reais |
| Custos | Medir implementação, execução, armazenamento, retenção e operação | Pendente de cenário |

### 8.4 Resultado

**Resultado:** CON-01 está arquiteturalmente analisada, mas o início de uma implementação definitiva permanece condicionado às decisões de finalidade, dados, segurança e operação.

## 9. Validação das visões C4 e sequências

### 9.1 Contexto C4

- apresenta as três personas oficiais;
- separa o núcleo do batch candidato;
- identifica a integração externa como alternativa;
- não introduz persona de dados ou ML no produto.

### 9.2 Contêineres

- interface, aplicação e persistência representam o núcleo;
- batch, artefatos e observabilidade estão marcados como candidatos;
- tecnologias não aprovadas permanecem neutras.

### 9.3 Componentes

- componentes do núcleo correspondem aos escopos funcionais;
- componentes batch representam capacidades conceituais;
- não há afirmação de fornecedor, framework de ML ou infraestrutura aprovada.

### 9.4 Sequência online

- autorização antecede a alteração;
- período e disponibilidade são validados;
- concorrência permanece com mecanismo a definir;
- estado inicial continua pendente;
- mudança de estado é relacionada à auditoria.

### 9.5 Sequência batch

- execução ao final do dia é representada;
- controle de execução, progresso, qualidade, treinamento e validação estão presentes;
- avanço do checkpoint permanece condicionado à política futura;
- falha e recuperação são representadas sem garantia inventada.

### 9.6 Inconsistências residuais

| Item | Impacto | Ação necessária |
|---|---|---|
| Estado inicial não definido | Afeta sequência e concorrência | Decisão de domínio |
| Limite estado-auditoria não definido | Afeta falha parcial | Experimento e ADR definitivo |
| Finalidade de CON-01 ausente | Afeta pipeline, métricas e promoção | Decisão de negócio |
| Dados novos sem semântica | Afeta checkpoint e idempotência | Experimento incremental |
| LGPD sem inventário | Impede dados reais | Avaliação de privacidade |
| Metas de carga ausentes | Impede decisões de escala/cache | Plano JMeter |

## 10. Validação da utility tree

A utility tree contempla 18 cenários:

| ID | Cenário | Atributo principal | Priorização |
|---|---|---|---|
| ATAM-01 | Solicitações simultâneas | Consistência | Alta/Alta |
| ATAM-02 | Conflito na agenda docente | Consistência | Alta/Média |
| ATAM-03 | Acesso indevido | Segurança | Alta/Alta |
| ATAM-04 | Falha estado-auditoria | Auditabilidade | Alta/Alta |
| ATAM-05 | Manutenção ou bloqueio | Disponibilidade | Alta/Média |
| ATAM-06 | Execução diária | Operabilidade | Alta/Média |
| ATAM-07 | Dados novos | Consistência batch | Alta/Alta |
| ATAM-08 | Falha parcial | Recuperabilidade | Alta/Alta |
| ATAM-09 | Jobs sobrepostos | Operabilidade | Alta/Alta |
| ATAM-10 | Degradação de dados | Qualidade de dados | Alta/Alta |
| ATAM-11 | Candidato pior | Confiabilidade ML | Alta/Alta |
| ATAM-12 | Rollback | Recuperabilidade ML | Alta/Alta |
| ATAM-13 | Indisponibilidade externa | Disponibilidade | Média/Média |
| ATAM-14 | Vazamento | Privacidade | Alta/Alta |
| ATAM-15 | Carga | Desempenho | Média/Alta |
| ATAM-16 | Evolução dos estados | Manutenibilidade | Média/Média |
| ATAM-17 | Movimentação inconsistente | Confiabilidade | Média/Média |
| ATAM-18 | Ausência de dados novos | Operabilidade batch | Média/Média |

**Resultado:** a utility tree cobre integralmente os estímulos expressamente exigidos e inclui cenários adicionais relevantes ao domínio.

## 11. Validação dos cenários ATAM

Cada cenário contém:

- fonte;
- estímulo;
- ambiente;
- artefato;
- resposta;
- métrica;
- origem;
- importância;
- dificuldade;
- decisão relacionada.

### 11.1 Métricas oficiais

- cobertura de linhas mínima de 80%;
- cobertura de branches mínima de 70%;
- 100% dos requisitos críticos rastreados;
- zero bugs críticos conhecidos;
- zero vulnerabilidades críticas conhecidas;
- exatamente uma reserva aceita sob concorrência;
- zero reservas conflitantes persistidas;
- zero mudanças de estado efetivadas sem auditoria correspondente.

### 11.2 Métricas tratadas como hipótese

- tolerância de atraso da execução diária;
- registros omitidos ou duplicados no batch;
- duração da recuperação;
- quantidade de retries;
- qualidade e drift dos dados;
- métricas e thresholds de modelo;
- tempo de rollback;
- volume de carga;
- percentis e taxa de erro;
- retenção de dados e artefatos.

**Resultado:** não foi identificada métrica inventada apresentada como requisito oficial.

## 12. Validação dos pontos de sensibilidade

Foram registrados pontos de sensibilidade relativos a:

- fronteira transacional;
- momento de revalidação;
- ocupação por `SOLICITADA`;
- autorização por objeto;
- consistência estado-auditoria;
- acoplamento externo;
- definição de dados novos;
- checkpoint;
- jobs sobrepostos;
- critérios de qualidade;
- métricas e promoção;
- logs, datasets e artefatos;
- complexidade tecnológica.

Os pontos estão vinculados a cenários e decisões.

## 13. Validação dos trade-offs

A arquitetura registra trade-offs entre:

- consistência e desempenho;
- revalidação e custo por operação;
- auditabilidade e simplicidade;
- cache e consistência;
- integração síncrona e desacoplada;
- batch integrado e separado;
- checkpoint simples e precisão;
- validação ampla e custo;
- promoção automática e revisão humana;
- retenção, privacidade e custo;
- infraestrutura dedicada e compartilhada;
- sofisticação técnica e prazo acadêmico.

**Resultado:** os trade-offs estão relacionados aos cenários e decisões correspondentes, sem ocultar efeitos negativos.

## 14. Validação dos riscos e não-riscos

### 14.1 Riscos confirmados

- mecanismo inadequado para RN-04;
- ausência de revalidação;
- inconsistência estado-auditoria;
- autorização apenas por perfil;
- estado inicial indefinido;
- CON-01 sem finalidade;
- omissão ou duplicação incremental;
- jobs sobrepostos;
- degradação não detectada;
- candidato pior promovido;
- rollback inviável;
- dados pessoais sem governança;
- falha externa propagada;
- movimentação inconsistente;
- infraestrutura excessiva;
- métricas prematuras.

### 14.2 Não-riscos condicionais

- Java 21 e Spring Boot 3.x;
- Testcontainers na persistência crítica;
- WireMock quando houver integração externa;
- separação lógica sem distribuição obrigatória;
- métricas desconhecidas mantidas como hipóteses;
- CON-01 separada da baseline;
- estado inicial mantido como pendência.

A classificação como não-risco não representa evidência de implementação nem imunidade a riscos futuros.

### 14.3 Temas de risco

1. Integridade transacional.
2. Segurança contextual.
3. Governança de CON-01.
4. Operação e recuperação.
5. Complexidade prematura.

## 15. Validação do painel multidisciplinar

### 15.1 Perspectivas contempladas

- arquitetura de solução;
- dados e ML;
- segurança e LGPD;
- operações e SRE;
- custos;
- facilitação ATAM.

### 15.2 Resultado por perspectiva

| Perspectiva | Resultado principal | Condicionante |
|---|---|---|
| Arquitetura | Estrutura lógica coerente e proporcional | Aprovar limites transacionais e modularidade |
| Dados/ML | Pipeline conceitualmente completo | Definir finalidade, dados, target e métricas |
| Segurança/LGPD | Riscos reconhecidos corretamente | Bloquear dados reais antes da avaliação LGPD |
| Operações/SRE | Falhas e operação foram analisadas | Definir estados do job, retry e observabilidade |
| Custos | Alternativas especializadas não são justificadas | Medir antes de escalar |
| ATAM | Cenários e riscos estão rastreados | Priorizar experimentos de alta importância/dificuldade |

## 16. Validação das divergências

Foram preservadas divergências sobre:

- lock, isolamento, constraint e controle otimista;
- mesma transação, outbox ou compensação para auditoria;
- batch no mesmo processo ou separado;
- timestamp, versão, CDC ou marcador composto;
- treinamento incremental ou dataset acumulado;
- promoção automática ou humana;
- logs mínimos ou ferramentas dedicadas;
- retenção ampla ou mínima;
- adoção de cache;
- consumo do modelo.

**Resultado:** as divergências não foram ocultadas. Cada consolidação mantém status, impacto e condição para decisão.

## 17. Validação dos ADRs

Foram registrados 14 ADRs:

1. estilo arquitetural do núcleo;
2. concorrência de reservas;
3. autorização contextual;
4. consistência estado-auditoria;
5. revalidação da disponibilidade;
6. separação lógica do batch;
7. identificação incremental e checkpoint;
8. coordenação de jobs e idempotência;
9. retry e recuperação;
10. qualidade, linhagem e reprodutibilidade;
11. gates, versionamento, promoção e rollback;
12. observabilidade do batch;
13. segurança e LGPD;
14. controle de custos.

Cada ADR contém:

- status;
- contexto;
- forças;
- alternativas;
- decisão ou condição de bloqueio;
- consequências positivas;
- consequências negativas;
- riscos;
- requisitos relacionados;
- cenários;
- evidência esperada.

**Resultado:** estrutura completa e adequada para evolução das decisões.

## 18. Validação da rastreabilidade

A matriz final relaciona:

`requisito → decisão → componente → evidência`

A rastreabilidade cobre:

- autenticação e autorização;
- período e disponibilidade;
- concorrência;
- manutenção e bloqueio;
- estados;
- auditoria;
- aprovação;
- retirada e devolução;
- notificação;
- relatórios;
- interface e erros;
- documentação pública;
- cobertura;
- defeitos;
- segurança;
- Testcontainers;
- teste concorrente;
- testes em camadas;
- CI;
- JMeter;
- CON-01.

### 18.1 Classificação da cobertura

| Classificação | Significado |
|---|---|
| Coberta arquiteturalmente | Existe abordagem coerente documentada |
| Mecanismo pendente | Resultado exigido, escolha técnica pendente |
| Parcial | Parte depende de decisão de negócio |
| Evidência não executada | Estratégia existe, resultado real ausente |
| Bloqueada | Não deve avançar antes de condição anterior |

## 19. Requisitos sem cobertura definitiva

- estado inicial e ocupação de reserva não restrita;
- transições alternativas e respectivos atores;
- diferença operacional entre bloqueio e manutenção;
- reservas existentes afetadas por indisponibilidade;
- critério de recurso restrito;
- responsabilidade exata do Responsável;
- alternativa e contrato de notificação;
- fórmulas e filtros dos relatórios;
- metas JMeter;
- viewports e critérios de acessibilidade;
- finalidade, dados, modelo, métricas e uso de CON-01.

Esses itens não representam omissão documental. Representam ausência de decisão nas fontes.

## 20. Decisões sem requisito explícito

- monólito modular;
- separação lógica ou física do batch;
- tecnologia e formato do checkpoint;
- mecanismo de exclusão de jobs;
- metadados operacionais do pipeline;
- armazenamento ou registry;
- promoção e rollback;
- observabilidade do batch;
- papel técnico responsável pelo modelo;
- cache de disponibilidade;
- infraestrutura dedicada.

Cada decisão foi classificada como proposta, candidata, pendente ou bloqueada.

## 21. Suposições controladas

| ID | Suposição | Risco se falsa | Tratamento |
|---|---|---|---|
| SUP-01 | Monólito modular atende a escala inicial | Redistribuição futura | Validar com JMeter |
| SUP-02 | Batch pode ficar fora do caminho online | Integração não documentada | Confirmar finalidade |
| SUP-03 | Fonte permite incrementalidade | CON-01 inviável ou inexato | Experimento de dados novos |
| SUP-04 | Versão anterior pode ser preservada | Rollback inviável | Definir versionamento |
| SUP-05 | Dados podem ser minimizados | Dataset insuficiente | Avaliação de privacidade e utilidade |
| SUP-06 | A equipe pode operar sinais mínimos | Falhas invisíveis | Definir responsabilidade operacional |

Nenhuma suposição possui status de requisito aprovado.

## 22. Perguntas abertas

### 22.1 Produto e domínio

1. Qual estado inicial assume uma reserva não restrita?
2. `SOLICITADA` ocupa os recursos?
3. Quais estados permitem alteração e cancelamento?
4. Quem inicia, conclui e registra não comparecimento?
5. Quando os recursos são liberados?
6. O que caracteriza recurso restrito?
7. Qual é a responsabilidade exata do Responsável?
8. Como bloqueio difere de manutenção?
9. Como tratar reservas existentes afetadas por indisponibilidade?
10. Como professor-usuário se relaciona com professor-recurso?

### 22.2 Integração, interface e qualidade

11. A notificação será simulada ou externa?
12. Quais evento, canal, destinatário, contrato e política de falha?
13. Quais fórmulas, filtros e permissões dos relatórios?
14. Quais metas de carga, percentis, taxa de erro e duração?
15. Quais viewports e critérios de acessibilidade?
16. Quais campos, visibilidade, retenção e imutabilidade da auditoria?

### 22.3 Dados e ML

17. Qual problema CON-01 resolve?
18. Qual valor o modelo oferece ao produto?
19. Quais dados podem ser utilizados?
20. O que significa dado novo para inclusão, atualização, correção e exclusão?
21. O treinamento é incremental ou utiliza dataset acumulado atualizado?
22. Qual algoritmo, target e conjunto de features?
23. Quais métricas e custos de erro?
24. Existe consumo online ou batch?
25. Como candidatos são validados, versionados e promovidos?
26. Quem autoriza promoção e rollback?
27. Qual retenção de datasets, metadados e artefatos?
28. Qual base legal e quais controles LGPD?

## 23. Riscos aceitos

Nenhum risco alto ou crítico foi automaticamente aceito pela revisão.

Uma aceitação futura deverá registrar:

- identificador;
- justificativa;
- responsável;
- controles compensatórios;
- impacto residual;
- evidência;
- prazo de revisão;
- ADR relacionada.

| Risco candidato | Condição mínima | Status |
|---|---|---|
| Latência adicional por revalidação | Resultado JMeter e preservação funcional | Não aceito |
| Complexidade estado-auditoria | Experimento e ADR definitivo | Não aceito |
| Atraso da execução batch | Tolerância operacional aprovada | Não aceito |
| Retenção limitada | LGPD, reprodução e custo avaliados | Não aceito |
| Promoção manual | Responsável e procedimento definidos | Não aceito |

## 24. Experimentos recomendados

| Ordem | Experimento | Cenários relacionados | Evidência esperada | Decisão habilitada |
|---|---|---|---|---|
| 1 | Concorrência de reservas | ATAM-01 | Exatamente uma aceita | Mecanismo de RN-04 |
| 2 | Falha estado-auditoria | ATAM-04 | Nenhum estado sem auditoria | ADR de consistência |
| 3 | Autorização por objeto | ATAM-03 | IDOR recusado | Autorização contextual |
| 4 | Revalidação na confirmação | ATAM-01/02/05 | Mudança concorrente recusada | Estratégia de disponibilidade |
| 5 | Dados novos | ATAM-07/18 | Inclusão, empate e atraso tratados | Checkpoint/watermark |
| 6 | Falha parcial | ATAM-08 | Progresso consistente | Recuperação e retry |
| 7 | Jobs sobrepostos | ATAM-09 | Uma execução compatível efetiva | Coordenação e idempotência |
| 8 | Degradação de dados | ATAM-10 | Lote inadequado bloqueado | Qualidade e gates |
| 9 | Candidato pior | ATAM-11 | Candidato não promovido | Política de promoção |
| 10 | Rollback | ATAM-12 | Versão anterior restaurada | Versionamento e rollback |
| 11 | LGPD do dataset | ATAM-14 | Inventário e controles aprovados | Uso de dados reais |
| 12 | Desempenho e custo | ATAM-15 | JMeter e medição de recursos | Cache, escala e infraestrutura |

## 25. Limitações

A revisão é exclusivamente documental.

Não foram executados:

- build;
- testes unitários;
- testes de integração;
- API black-box;
- end-to-end;
- Testcontainers;
- WireMock;
- teste concorrente;
- GitHub Actions;
- JaCoCo;
- SonarCloud;
- JMeter;
- renderização Mermaid/C4;
- processamento batch;
- validação de dataset;
- treinamento;
- promoção;
- rollback.

Os resultados registrados representam cobertura documental, respostas arquiteturais esperadas, decisões propostas e hipóteses de avaliação.

## 26. Conclusão consolidada

A revisão conclui que `docs/arquitetura.md` apresenta uma arquitetura abrangente, rastreável e coerente com os requisitos disponíveis do sistema Organização de Recursos.

A arquitetura:

- preserva as fontes oficiais;
- mantém as personas e autorizações coerentes;
- protege as regras críticas do domínio;
- diferencia requisitos, alternativas, decisões e hipóteses;
- cobre o núcleo online e CON-01;
- relaciona diagramas, sequências, pipeline, utility tree e riscos;
- contempla integralmente os cenários críticos solicitados;
- registra sensibilidades e trade-offs;
- conserva divergências relevantes;
- formaliza decisões em ADRs;
- identifica lacunas e bloqueios;
- mantém riscos altos e críticos sem aceitação automática;
- define experimentos proporcionais para evolução das decisões.

**Conclusão:** o conjunto arquitetural está adequado para deliberação da equipe, planejamento de implementação e execução dos experimentos prioritários. A aprovação operacional definitiva permanece condicionada às decisões de domínio, aos resultados dos experimentos e às evidências reais de qualidade, segurança, desempenho e operação.

## 27. Revisão após a auditoria final

### 27.1 Conclusão anterior preservada

O relatório anterior concluiu que a arquitetura estava adequada para deliberação, mas ainda condicionada a decisões, experimentos e evidências futuras. Essa conclusão histórica não é apagada.

### 27.2 Correção de interpretação

A ausência de implementação, teste executado, build, pipeline, treinamento ou medição não é, isoladamente, uma falha documental nesta atividade, pois o escopo da correção proíbe implementação, testes e execução de comandos. As evidências necessárias, métricas, critérios esperados, experimentos pendentes e condições de revisão já estavam registrados nas seções 20, 31, 36, 37 e 44 deste relatório e foram detalhados nas seções 46 a 50 de `docs/arquitetura.md`.

Permanece pendência legítima quando falta uma decisão humana, uma métrica de negócio ou informação de origem. Esses itens não foram convertidos em fatos.

### 27.3 Correções realizadas

- Reclassificação da ausência de execução como não aplicável ao escopo documental, sem fabricar resultado.
- Inclusão das invariantes do batch com status parcial e validação pendente.
- Inclusão dos cenários ATAM-19 a ATAM-27 para reexecução, duplicação/esquema, janela, promoção incompleta, registry, impacto online, uso indevido, custo e dados tardios.
- Inclusão de justificativa de prioridade na utility tree complementar.
- Inclusão de táticas de Len Bass como intenção arquitetural, sem tratar ferramenta como tática.
- Inclusão de matriz suplementar separando evidência planejada de evidência executada.
- Preservação de alternativas, divergências, suposições e riscos sem aceite.

### 27.4 Conclusão atual

**Resultado documental:** completo quanto ao plano arquitetural, à identificação de lacunas, à avaliação ATAM, ao painel, às táticas e ao plano de rastreabilidade.

**Resultado decisório:** parcial, porque decisões humanas, métricas e experimentos identificados como pendentes permanecem pendentes por determinação dos próprios artefatos. Não há evidência executada registrada, e isso não é apresentado como resultado.
