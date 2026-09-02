# Relatório de Validação da Arquitetura

## 1. Identificação

- **Documento avaliado:** `docs/arquitetura.md`
- **Produto:** Organização de Recursos
- **Tipo de avaliação:** revisão documental de arquitetura com aplicação do método ATAM
- **Status:** concluído com pendências de decisão registradas
- **Data:** 2026-09-02
- **Resultado geral:** adequado para revisão e deliberação da equipe

## 2. Objetivo da validação

Este relatório registra o resultado da revisão documental de `docs/arquitetura.md`, verificando:

- aderência aos requisitos e regras de negócio;
- identificação dos drivers arquiteturais;
- cobertura dos atributos de qualidade prioritários;
- coerência entre os fluxos online e batch;
- qualidade da avaliação ATAM;
- separação entre fatos, hipóteses, alternativas e decisões;
- rastreabilidade entre cenários, decisões, sensibilidades, trade-offs e riscos;
- preservação das pendências que dependem de decisão da equipe.

A validação não modifica os requisitos do produto e não converte alternativas arquiteturais em decisões aprovadas.

## 3. Fontes consideradas

A revisão documental considerou:

- `docs/prd.md`;
- `docs/fluxos-personas.md`;
- `docs/arquitetura.md`;
- personas oficiais referenciadas pela documentação;
- CON-01, registrada como restrição adicional do exercício arquitetural.

As fontes oficiais do produto permanecem separadas das decisões e análises arquiteturais.

## 4. Escopo avaliado

A avaliação cobriu:

1. contexto, objetivo e limites do produto;
2. stakeholders e personas oficiais;
3. requisitos arquiteturalmente significativos;
4. atributos de qualidade;
5. drivers priorizados;
6. riscos iniciais;
7. responsabilidades, limites e interfaces;
8. fluxo online de reservas;
9. processamento batch associado a CON-01;
10. diagramas de contexto, contêineres e componentes;
11. identificação e processamento de dados novos;
12. watermark e checkpoint;
13. idempotência;
14. prevenção de jobs sobrepostos;
15. retry e recuperação;
16. qualidade e linhagem de dados;
17. reprodutibilidade;
18. validação do candidato;
19. versionamento, promoção e rollback;
20. observabilidade;
21. segurança, privacidade e LGPD;
22. custos;
23. utility tree;
24. cenários de atributos de qualidade;
25. pontos de sensibilidade;
26. trade-offs;
27. riscos, não-riscos e temas de risco;
28. rastreabilidade entre cenários e decisões.

## 5. Resultado da validação

A revisão documental concluiu que `docs/arquitetura.md` apresenta uma avaliação arquitetural coerente com os requisitos disponíveis e adequada ao método ATAM.

O documento:

- preserva os requisitos e as regras de negócio;
- diferencia a baseline do produto da restrição adicional CON-01;
- não incorpora funcionalidades do projeto demonstrativo Foot Fanatics;
- utiliza somente Solicitante, Responsável e Administrador como personas oficiais;
- mantém papéis técnicos separados das personas do produto;
- identifica drivers e atributos de qualidade prioritários;
- apresenta abordagens arquiteturais sem tratá-las automaticamente como aprovadas;
- estrutura uma utility tree com importância e dificuldade;
- registra cenários completos de atributos de qualidade;
- vincula cenários a requisitos, decisões, sensibilidades, trade-offs e riscos;
- preserva métricas não aprovadas como hipóteses pendentes;
- mantém as decisões de negócio não especificadas como pendências;
- não declara implementação, testes ou ferramentas como executados.

## 6. Validação das fontes e regras críticas

### 6.1 Personas e autorização

A arquitetura mantém como personas oficiais:

- Solicitante;
- Responsável;
- Administrador.

A autorização foi tratada como responsabilidade do back-end, considerando perfil, propriedade do objeto e responsabilidade operacional.

A revisão confirmou que:

- o Solicitante opera somente suas próprias reservas;
- somente o Responsável autorizado aprova recursos restritos;
- o Administrador não substitui o Responsável;
- a diferenciação entre professor como usuário e professor como recurso permanece registrada;
- a relação cadastral entre professor-usuário e professor-recurso permanece pendente.

### 6.2 Concorrência e consistência

RN-04 foi interpretada corretamente como requisito de resultado:

> Duas solicitações simultâneas para o mesmo recurso e período devem produzir exatamente uma reserva aceita.

A arquitetura não transforma uma técnica específica em requisito obrigatório.

Permanecem como alternativas:

- restrição no banco;
- isolamento transacional;
- lock pessimista;
- controle otimista;
- estrutura de slots;
- outra estratégia que demonstre o resultado exigido.

A seleção do mecanismo permanece dependente de experimento com persistência realista.

### 6.3 Estados e auditoria

A arquitetura preserva os estados oficiais:

- `SOLICITADA`;
- `APROVADA`;
- `EM_USO`;
- `CONCLUIDA`;
- `REJEITADA`;
- `CANCELADA`;
- `NAO_COMPARECEU`.

Também mantém como pendentes:

- estado inicial da reserva não restrita;
- ocupação de recursos por `SOLICITADA`;
- atores e condições das transições não detalhadas;
- liberação de recursos;
- relação entre devolução e conclusão.

RN-08 permanece limitada à proibição de apagar reservas iniciadas.

RN-09 permanece limitada à exigência de auditoria para mudanças de estado da reserva. A auditoria de eventos técnicos do processamento batch é tratada como decisão arquitetural candidata, e não como obrigação derivada de RN-09.

### 6.4 Persistência e testes

RNF-07 foi interpretada corretamente como exigência de testes da persistência crítica em banco containerizado com Testcontainers.

A arquitetura não trata RNF-07 como exigência de:

- réplica de leitura;
- banco específico;
- isolamento específico;
- armazenamento distribuído;
- arquitetura de alta disponibilidade.

O documento mantém o teste automatizado de concorrência como evidência indispensável para RN-04 e RNF-09.

## 7. Validação de CON-01

CON-01 está registrada como restrição adicional com três fatos confirmados:

1. existe uma execução diária;
2. a execução ocorre ao final do dia;
3. o processo treina ou retreina usando somente dados novos.

A arquitetura não presume:

- finalidade do modelo;
- problema de negócio;
- variável-alvo;
- algoritmo;
- features;
- volume dos dados;
- tecnologia de agendamento;
- armazenamento;
- integração com o fluxo online;
- métricas de validação;
- promoção automática;
- rollback automático.

Esses elementos permanecem como decisões pendentes.

## 8. Validação da utility tree

A utility tree identifica e prioriza:

- consistência de reservas;
- conflito na agenda do professor;
- autorização contextual;
- auditabilidade;
- manutenção e bloqueio;
- execução diária;
- identificação de dados novos;
- recuperação de falha parcial;
- jobs sobrepostos;
- degradação de dados;
- candidato pior;
- rollback;
- indisponibilidade externa;
- vazamento de dados;
- comportamento sob carga;
- evolução da política de estados;
- integridade de retirada e devolução;
- execução sem dados novos.

Cada cenário possui classificação preliminar de importância e dificuldade.

## 9. Validação dos cenários ATAM

Os cenários foram estruturados com:

- fonte;
- estímulo;
- ambiente;
- artefato;
- resposta;
- métrica;
- origem;
- importância;
- dificuldade;
- decisões relacionadas.

Foram documentados os seguintes cenários:

| ID | Cenário | Cobertura principal |
|---|---|---|
| ATAM-01 | Duas solicitações simultâneas | Concorrência e consistência |
| ATAM-02 | Conflito na agenda do professor | Disponibilidade docente |
| ATAM-03 | Acesso indevido | Segurança e IDOR |
| ATAM-04 | Falha entre estado e auditoria | Auditabilidade |
| ATAM-05 | Manutenção ou bloqueio | Disponibilidade operacional |
| ATAM-06 | Execução diária do batch | Operabilidade |
| ATAM-07 | Processamento somente de dados novos | Incrementalidade |
| ATAM-08 | Falha parcial do batch | Recuperabilidade |
| ATAM-09 | Jobs sobrepostos | Concorrência batch |
| ATAM-10 | Degradação dos dados | Qualidade de dados |
| ATAM-11 | Candidato pior | Confiabilidade de modelo |
| ATAM-12 | Rollback de versão | Recuperabilidade de modelo |
| ATAM-13 | Indisponibilidade externa | Integração e disponibilidade |
| ATAM-14 | Vazamento de dados | Segurança e LGPD |
| ATAM-15 | Operação sob carga | Desempenho |
| ATAM-16 | Alteração da política de estados | Manutenibilidade |
| ATAM-17 | Movimentação inconsistente | Integridade operacional |
| ATAM-18 | Execução sem dados novos | Operabilidade batch |

## 10. Tratamento das métricas

As métricas respaldadas pela baseline permanecem como valores oficiais:

- cobertura de linhas mínima de 80%;
- cobertura de branches mínima de 70%;
- 100% dos requisitos críticos rastreados;
- zero bugs críticos conhecidos;
- zero vulnerabilidades críticas conhecidas;
- exatamente uma reserva aceita em cenário simultâneo;
- zero reservas conflitantes persistidas no cenário concorrente;
- zero mudanças de estado efetivadas sem auditoria correspondente.

Valores não definidos pelas fontes foram corretamente classificados como:

`HIPÓTESE PENDENTE DE DECISÃO DA EQUIPE`

Essa classificação foi aplicada a:

- tolerância de atraso do job;
- quantidade de retries;
- duração máxima da execução;
- limites de qualidade dos dados;
- métricas do modelo;
- critérios de promoção;
- tempo de rollback;
- volume de carga;
- percentis de resposta;
- taxa de erro;
- retenção de dados e artefatos.

## 11. Pontos de sensibilidade

A avaliação identificou como principais pontos de sensibilidade:

- fronteira transacional da reserva;
- momento da revalidação de disponibilidade;
- ocupação de recursos por `SOLICITADA`;
- autorização por objeto;
- consistência entre estado e auditoria;
- acoplamento da integração externa;
- definição de dados novos;
- checkpoint e recuperação;
- coordenação de jobs sobrepostos;
- critérios de qualidade dos dados;
- validação e promoção do candidato;
- conteúdo de logs, datasets e artefatos;
- complexidade das tecnologias candidatas.

Os pontos de sensibilidade estão vinculados aos cenários e às decisões correspondentes.

## 12. Trade-offs

A análise registra trade-offs entre:

- consistência e desempenho;
- revalidação e custo por requisição;
- auditabilidade e simplicidade transacional;
- cache e consistência;
- integração síncrona e desacoplamento;
- batch integrado e batch separado;
- simplicidade do checkpoint e precisão incremental;
- validação ampla e custo de processamento;
- promoção automática e revisão humana;
- retenção, privacidade e custo;
- infraestrutura dedicada e compartilhada;
- sofisticação arquitetural e prazo acadêmico.

Os trade-offs permanecem relacionados aos drivers, cenários e decisões arquiteturais.

## 13. Riscos arquiteturais

A revisão confirmou riscos relacionados a:

- técnica de concorrência inadequada;
- ausência de revalidação na confirmação;
- inconsistência entre estado e auditoria;
- autorização baseada somente em perfil;
- estado inicial não definido;
- implementação de CON-01 sem finalidade;
- omissão ou duplicação de dados no processamento incremental;
- sobreposição de jobs;
- degradação de dados não detectada;
- promoção de candidato pior;
- impossibilidade de rollback;
- tratamento de dados pessoais sem governança;
- indisponibilidade externa propagada para o fluxo principal;
- inconsistência em retirada e devolução;
- infraestrutura desproporcional;
- adoção de métricas não aprovadas.

Os riscos estão vinculados aos cenários e às decisões relacionadas.

## 14. Não-riscos identificados

A avaliação classificou como não-riscos, nas condições documentadas:

- uso de Java 21 e Spring Boot 3.x;
- uso de Testcontainers para persistência crítica;
- uso de WireMock quando houver integração externa;
- separação lógica de módulos sem distribuição obrigatória;
- manutenção de métricas desconhecidas como hipóteses;
- separação de CON-01 da baseline oficial;
- preservação do estado inicial como pendência.

A classificação como não-risco não representa implementação concluída, teste executado ou ausência absoluta de risco futuro.

## 15. Temas de risco

Os riscos foram consolidados em cinco temas:

1. **Integridade transacional**
   - concorrência;
   - revalidação;
   - estado e auditoria;
   - estado inicial.

2. **Segurança contextual**
   - autorização por objeto;
   - privacidade;
   - integração externa;
   - exposição em logs e erros.

3. **Governança de CON-01**
   - finalidade;
   - dados;
   - incrementalidade;
   - métricas;
   - promoção;
   - rollback.

4. **Operação e recuperação**
   - falha parcial;
   - checkpoint;
   - jobs sobrepostos;
   - degradação dos dados;
   - observabilidade.

5. **Complexidade prematura**
   - infraestrutura excessiva;
   - tecnologias sem necessidade demonstrada;
   - metas não aprovadas;
   - impacto sobre o prazo acadêmico.

## 16. Pendências preservadas

Permanecem pendentes de decisão:

- estado inicial de reserva não restrita;
- ocupação de recursos por `SOLICITADA`;
- transições, atores e condições não especificados;
- mecanismo técnico para RN-04;
- tratamento de reservas existentes afetadas por indisponibilidade;
- critério de recurso restrito;
- responsabilidade exata do Responsável;
- política de auditoria operacional;
- alternativa e contrato de notificação;
- fórmulas e filtros dos relatórios;
- metas do teste de carga;
- viewports e critérios de acessibilidade;
- propósito do treinamento;
- definição de dados novos;
- checkpoint e idempotência;
- política de retry e recuperação;
- validação e gates do candidato;
- versionamento, promoção e rollback;
- observabilidade;
- análise LGPD;
- custos do processamento batch.

## 17. Limitações da validação

A avaliação realizada é exclusivamente documental.

Não foram executados:

- build da aplicação;
- testes unitários;
- testes de integração;
- testes de API;
- testes end-to-end;
- Testcontainers;
- WireMock;
- testes de concorrência;
- GitHub Actions;
- JaCoCo;
- SonarCloud;
- JMeter;
- renderização dos diagramas Mermaid/C4;
- experimentos de checkpoint;
- testes de jobs sobrepostos;
- validação de dados;
- treinamento de modelo;
- promoção ou rollback.

Os resultados descritos no documento representam requisitos, respostas arquiteturais esperadas e hipóteses de avaliação, não evidências de execução.

## 18. Conclusão

A revisão documental conclui que `docs/arquitetura.md` apresenta cobertura adequada dos drivers, atributos de qualidade, abordagens e cenários arquiteturais relevantes ao sistema Organização de Recursos.

A avaliação ATAM:

- preserva as fontes oficiais;
- não introduz métricas como fatos;
- cobre os cenários prioritários do núcleo e de CON-01;
- registra sensibilidades e trade-offs;
- diferencia riscos e não-riscos;
- consolida temas de risco;
- mantém rastreabilidade entre requisitos, cenários e decisões;
- preserva explicitamente as decisões que dependem de validação humana.

O artefato está adequado para orientar decisões arquiteturais e experimentos posteriores, sem representar aprovação automática das alternativas técnicas registradas.