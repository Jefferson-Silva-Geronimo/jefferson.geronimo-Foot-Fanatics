# PRD - Organização de Recursos

## 1. Controle do Documento

- **Finalidade:** consolidar a elicitação de requisitos do sistema Organização de Recursos a partir das três personas oficiais e do escopo oficial fornecido.
- **Status do documento:** Baseline para revisão da equipe.
- **Versão:** 1.0.
- **Origem da elicitação:** personas oficiais, requisitos funcionais mínimos, regras críticas, estratégia obrigatória de qualidade e escopos oficiais desta solicitação.
- **Arquivos utilizados:** `docs/personas/solicitante.md`, `docs/personas/responsavel.md`, `docs/personas/administrador.md`.
- **Data da geração:** 2026-08-28.
- **Observação:** a baseline deve ser revisada e aprovada pela equipe. Decisões ainda não especificadas permanecem em pendências ou como candidatos não aprovados.

## 2. Visão Geral do Produto

### Problema

A alocação de salas, professores e materiais precisa ocorrer sem conflitos de horário e com controle sobre recursos restritos, manutenção, retiradas, devoluções e mudanças realizadas.

### Objetivo

Desenvolver e validar uma aplicação que organize a alocação de salas, professores e materiais sem conflitos de horário, produzindo evidências objetivas de qualidade, segurança, rastreabilidade e desempenho.

### Valor esperado

- Evitar sobreposição de reservas, inclusive na agenda do professor.
- Impedir dupla reserva em solicitações simultâneas.
- Controlar aprovação de recursos restritos e indisponibilidade por manutenção.
- Registrar retiradas, devoluções e mudanças para rastreabilidade e auditoria.
- Apoiar o controle operacional por meio de relatórios.

### Limites do produto

O produto cobre somente os perfis Solicitante, Responsável e Administrador e os escopos E1 a E13 definidos neste documento. Não incorpora funcionalidades, entidades ou escopos do projeto demonstrativo Foot Fanatics.

## 3. Escopo

### 3.1 Dentro do escopo

- **E1: Acesso e Perfis**
- **E2: Cadastro de Recursos**
- **E3: Pesquisa e Disponibilidade**
- **E4: Reservas e Agenda**
- **E5: Aprovação de Recursos Restritos**
- **E6: Manutenção e Bloqueios**
- **E7: Retirada e Devolução de Materiais**
- **E8: Auditoria e Histórico**
- **E9: Notificações e Integrações**
- **E10: Relatórios**
- **E11: Interface, Erros e Acessibilidade**
- **E12: Documentação da API ou Fluxos Públicos**
- **E13: Qualidade, Segurança, Desempenho e CI**

### 3.2 Fora do escopo

- Funcionalidades do Foot Fanatics.
- Perfis diferentes de Solicitante, Responsável e Administrador.
- Funcionalidades não respaldadas pelos requisitos oficiais.
- Decisões de negócio ainda não aprovadas pela equipe.
- Dados pessoais ou biográficos das personas, como nome, idade, foto, renda ou biografia.

## 4. Personas Utilizadas

### Solicitante

- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Objetivo:** organizar suas reservas de salas, professores e materiais sem conflitos de horário.
- **Responsabilidades:** consultar disponibilidade; criar suas reservas; alterar suas reservas; cancelar suas reservas.
- **Permissões:** consultar recursos e pesquisar disponibilidade; criar, alterar e cancelar suas reservas.
- **Restrições:** não pode operar reservas de outros solicitantes; reservar recursos em manutenção; gerar dupla reserva; aprovar solicitações especiais; validar docentes; gerenciar salas, professores, materiais, usuários, bloqueios ou manutenção.
- **Funcionalidades relacionadas:** autenticação e autorização, consulta de recursos, pesquisa de disponibilidade, criação, alteração e cancelamento de reservas.

### Responsável

- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Objetivo:** garantir aprovação de solicitações especiais, validação da alocação de docentes e acompanhamento de materiais.
- **Responsabilidades:** aprovar solicitações especiais; validar docentes; acompanhar retiradas; acompanhar devoluções.
- **Permissões:** aprovar solicitações especiais; validar a alocação de docentes; acompanhar e registrar retiradas e devoluções de materiais.
- **Restrições:** não pode gerenciar salas, professores, materiais, usuários, bloqueios ou manutenção; operar reservas de outros solicitantes; aprovar recursos restritos fora de sua responsabilidade.
- **Funcionalidades relacionadas:** autenticação e autorização, aprovação, validação de docentes, registro de retirada e registro de devolução de materiais.

### Administrador

- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Objetivo:** manter recursos, usuários, bloqueios e manutenção organizados para alocação sem conflitos.
- **Responsabilidades:** gerenciar salas, professores, materiais, usuários, bloqueios e períodos de manutenção.
- **Permissões:** gerenciar esses cadastros e consultar relatórios e histórico auditável.
- **Restrições:** não pode permitir conflitos, reservas em manutenção ou apagar reservas iniciadas; não pode substituir a aprovação de solicitações especiais atribuída aos Responsáveis.
- **Funcionalidades relacionadas:** autenticação e autorização, gestão de salas, professores, materiais, usuários, bloqueios e manutenção, relatórios e histórico auditável.

## 5. Premissas, Dependências e Restrições

### Fatos oficiais

- A aplicação será desenvolvida em equipe com Java 21 e Spring Boot 3.x.
- A entrega está prevista para a semana 46.
- O sistema deve organizar salas, professores e materiais sem conflitos de horário.
- Os perfis oficiais são somente Solicitante, Responsável e Administrador.
- O término da reserva deve ser posterior ao início.
- A sobreposição aplica-se a sala, material e professor.
- Solicitações simultâneas para o mesmo recurso e período devem aceitar somente uma reserva.
- Recursos em manutenção não podem ser reservados.
- Recursos restritos exigem aprovação e somente Responsável pode aprová-los.
- O fluxo principal é `SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA`.
- Estados alternativos oficiais: `REJEITADA`, `CANCELADA` e `NAO_COMPARECEU`.
- Reservas iniciadas não podem ser apagadas.
- Toda mudança de estado deve gerar auditoria.
- A qualidade deve considerar JUnit 5, testes parametrizados, integração, API em caixa-preta, end-to-end, Testcontainers, WireMock, concorrência automatizada, TDD ou BDD, GitHub Actions em pull requests, JaCoCo, SonarCloud e JMeter.
- Metas oficiais: 80% de cobertura de linhas, 70% de cobertura de branches, 100% dos requisitos críticos rastreados, zero bugs críticos conhecidos e zero vulnerabilidades críticas conhecidas.

### Dependências oficiais

- Banco de dados containerizado com Testcontainers para validação de persistência crítica.
- WireMock para integrações externas.
- GitHub Actions executado em pull requests.
- JaCoCo, SonarCloud e JMeter para as evidências de qualidade definidas.

### Hipóteses e limites

Não há hipóteses de negócio aprovadas além dos fatos acima. Metas de desempenho, responsividade, acessibilidade, disponibilidade, retenção de auditoria, canal de notificação e transições não especificadas precisam de decisão humana e estão registradas nas seções 13 e 14.

## 6. Regras de Negócio

### RN-01: Ordem temporal da reserva

- **Descrição:** o término da reserva deve ser posterior ao início.
- **Origem:** regras críticas de tempo e concorrência.
- **RFs relacionados:** RF-10, RF-11.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes unitários e de API com intervalo válido e inválido, incluindo testes parametrizados.

### RN-02: Não sobreposição do mesmo recurso

- **Descrição:** reservas do mesmo recurso não podem se sobrepor.
- **Origem:** regras críticas de tempo e concorrência.
- **RFs relacionados:** RF-09, RF-10, RF-11, RF-13.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes de integração, API e end-to-end com sala, material e professor.

### RN-03: Agenda do professor

- **Descrição:** a regra de sobreposição também se aplica à agenda do professor alocado.
- **Origem:** regras críticas de tempo e concorrência.
- **RFs relacionados:** RF-09, RF-10, RF-11, RF-13.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes de integração e API com reservas que conflitam somente na agenda do professor.

### RN-04: Unicidade sob concorrência

- **Descrição:** duas solicitações simultâneas para o mesmo recurso e período devem produzir somente uma reserva aceita.
- **Origem:** regras críticas de tempo e concorrência.
- **RFs relacionados:** RF-10, RF-13.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** teste automatizado de concorrência contra banco em Testcontainers.

### RN-05: Indisponibilidade por manutenção

- **Descrição:** recursos em manutenção não podem ser reservados.
- **Origem:** regras críticas de tempo e concorrência e personas.
- **RFs relacionados:** RF-07, RF-09, RF-10, RF-11.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes de API, integração e end-to-end para recurso em período de manutenção.

### RN-06: Aprovação de recursos restritos

- **Descrição:** recursos restritos exigem aprovação; somente o perfil Responsável pode aprová-los.
- **Origem:** regras críticas de estados e auditoria e personas.
- **RFs relacionados:** RF-01, RF-10, RF-15.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes positivos e negativos de autorização e fluxo de aprovação.

### RN-07: Fluxo de estados

- **Descrição:** o fluxo principal é `SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA`; estados alternativos oficiais são `REJEITADA`, `CANCELADA` e `NAO_COMPARECEU`.
- **Origem:** regras críticas de estados e auditoria.
- **RFs relacionados:** RF-10, RF-15, RF-19, RF-20.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** testes de API e end-to-end dos estados e das transições especificadas.

### RN-08: Reserva iniciada não pode ser apagada

- **Descrição:** reservas iniciadas não podem ser apagadas.
- **Origem:** regras críticas de estados e auditoria e personas.
- **RFs relacionados:** RF-12, RF-19.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** teste de autorização e de erro ao tentar apagar/cancelar reserva iniciada.

### RN-09: Auditoria de mudança de estado

- **Descrição:** toda mudança de estado deve gerar registro de auditoria.
- **Origem:** regras críticas de estados e auditoria e personas.
- **RFs relacionados:** RF-19, RF-20.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** teste de integração com persistência realista e consulta do histórico.

### RN-10: Rastreabilidade dos requisitos críticos

- **Descrição:** todos os requisitos críticos devem estar rastreados na matriz de rastreabilidade.
- **Origem:** estratégia obrigatória de qualidade.
- **RFs/RNFs relacionados:** todos os requisitos críticos.
- **Criticidade:** crítica.
- **Evidência de validação esperada:** matriz completa e revisão cruzada do Analyst, Product Manager, QA e Architect.

## 7. Requisitos Funcionais

### RF-01: Autenticação e autorização por perfil

- **Descrição:** O sistema deve autenticar usuários e autorizar as ações conforme os perfis Solicitante, Responsável e Administrador.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante, Responsável e Administrador.
- **Arquivo de origem:** `docs/personas/solicitante.md`, `docs/personas/responsavel.md`, `docs/personas/administrador.md`.
- **Seção de origem:** Funcionalidades Utilizadas, Permissões e Restrições.
- **Escopo principal:** E1: Acesso e Perfis.
- **Escopos relacionados:** E5: Aprovação de Recursos Restritos; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 1. Autenticação e autorização por perfil.
- **Regras de negócio relacionadas:** RN-06.
- **Pré-condições:** usuário possui credenciais e perfil cadastrado.
- **Resultado esperado:** acesso permitido somente às ações autorizadas para o perfil autenticado.
- **Evidência esperada:** testes de autenticação e autorização com casos positivos e negativos para os três perfis.

#### Critérios de aceitação

1. Dado que um usuário autenticado possui um dos três perfis oficiais,
   Quando acessa uma funcionalidade permitida ao seu perfil,
   Então o sistema permite a operação.

2. Dado que um usuário autenticado tenta executar uma ação não permitida ao seu perfil,
   Quando solicita a operação,
   Então o sistema recusa a operação e apresenta uma mensagem de erro compreensível.

#### Métrica funcional

- **Nome:** Taxa de acesso permitido e acesso recusado corretos
- **Definição:** Percentual de operações que recebem resposta correta conforme autorização do perfil
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada operação autorizada e não autorizada testada para os três perfis
- **Método de validação:** Testes de API black-box com casos positivos e negativos
- **Critério de aprovação:** 100% das operações recebem resposta esperada (permitidas=permitidas, recusadas=recusadas)

### RF-02: Gestão de salas

- **Descrição:** O sistema deve permitir ao Administrador cadastrar e consultar salas.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E2: Cadastro de Recursos.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E6: Manutenção e Bloqueios.
- **Requisito oficial relacionado:** 2. Cadastro e consulta de salas, professores e materiais.
- **Regras de negócio relacionadas:** RN-05.
- **Pré-condições:** Administrador autenticado.
- **Resultado esperado:** sala cadastrada ou consultada fica disponível para as operações autorizadas.
- **Evidência esperada:** testes de API e integração de cadastro e consulta.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado,
   Quando cadastra uma sala,
   Então o sistema registra a sala e permite sua consulta.

2. Dado que um Solicitante não possui permissão de gestão,
   Quando tenta cadastrar uma sala,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de salas cadastradas consultáveis
- **Definição:** Percentual de salas cadastradas que podem ser consultadas corretamente
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada sala cadastrada por Administrador autenticado
- **Método de validação:** Testes de API de cadastro e consulta com Testcontainers
- **Critério de aprovação:** 100% das salas cadastradas são consultáveis após cadastro

### RF-03: Gestão de professores

- **Descrição:** O sistema deve permitir ao Administrador cadastrar e consultar professores.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E2: Cadastro de Recursos.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Requisito oficial relacionado:** 2. Cadastro e consulta de salas, professores e materiais.
- **Regras de negócio relacionadas:** RN-03.
- **Pré-condições:** Administrador autenticado.
- **Resultado esperado:** professor cadastrado ou consultado pode ser considerado na pesquisa e na agenda.
- **Evidência esperada:** testes de API e integração de cadastro, consulta e uso na agenda.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado,
   Quando cadastra um professor,
   Então o sistema registra o professor e permite sua consulta.

2. Dado que um Solicitante não possui permissão de gestão,
   Quando tenta cadastrar um professor,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de professores cadastrados consultáveis e alocáveis
- **Definição:** Percentual de professores cadastrados que podem ser consultados e têm agenda disponível para validação
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada professor cadastrado com agenda sem conflito
- **Método de validação:** Testes de API de cadastro, consulta e validação de agenda
- **Critério de aprovação:** 100% dos professores cadastrados são consultáveis e têm agenda validável

### RF-04: Gestão de materiais

- **Descrição:** O sistema deve permitir ao Administrador cadastrar e consultar materiais.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E2: Cadastro de Recursos.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E7: Retirada e Devolução de Materiais.
- **Requisito oficial relacionado:** 2. Cadastro e consulta de salas, professores e materiais.
- **Regras de negócio relacionadas:** RN-05.
- **Pré-condições:** Administrador autenticado.
- **Resultado esperado:** material cadastrado ou consultado fica disponível para alocação e movimentação autorizadas.
- **Evidência esperada:** testes de API e integração de cadastro, consulta e uso em reserva.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado,
   Quando cadastra um material,
   Então o sistema registra o material e permite sua consulta.

2. Dado que um Solicitante não possui permissão de gestão,
   Quando tenta cadastrar um material,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de materiais cadastrados consultáveis e reserváveis
- **Definição:** Percentual de materiais cadastrados que podem ser consultados e utilizados em reservas
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada material cadastrado por Administrador autenticado
- **Método de validação:** Testes de API de cadastro, consulta e uso em reserva
- **Critério de aprovação:** 100% dos materiais cadastrados são consultáveis e reserváveis

### RF-05: Gestão de usuários

- **Descrição:** O sistema deve permitir ao Administrador gerenciar usuários e seus perfis oficiais.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E1: Acesso e Perfis.
- **Escopos relacionados:** E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 1. Autenticação e autorização por perfil.
- **Regras de negócio relacionadas:** RN-06.
- **Pré-condições:** Administrador autenticado.
- **Resultado esperado:** usuários e os três perfis oficiais ficam gerenciados para autenticação e autorização.
- **Evidência esperada:** testes de API e autorização para gestão de usuários.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado,
   Quando gerencia um usuário com um perfil oficial,
   Então o sistema registra a alteração para uso na autorização.

2. Dado que um usuário não é Administrador,
   Quando tenta gerenciar usuários,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de usuários gerenciados com perfil oficial correto
- **Definição:** Percentual de usuários associados aos perfis oficiais (Solicitante, Responsável, Administrador)
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada usuário gerenciado por Administrador
- **Método de validação:** Testes de API de gerenciamento e autorização com autenticação
- **Critério de aprovação:** 100% dos usuários possuem perfil oficial único; nenhum perfil adicionado fora dos três oficiais

### RF-06: Gestão de bloqueios

- **Descrição:** O sistema deve permitir ao Administrador gerenciar bloqueios de recursos.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E6: Manutenção e Bloqueios.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Requisito oficial relacionado:** 8. Bloqueio de recursos em manutenção.
- **Regras de negócio relacionadas:** RN-05.
- **Pré-condições:** Administrador autenticado e recurso cadastrado.
- **Resultado esperado:** o bloqueio gerenciado é considerado na disponibilidade e nas reservas.
- **Evidência esperada:** testes de API e integração de criação e consulta de bloqueio.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado e o recurso existe,
   Quando cria um bloqueio para o recurso,
   Então o sistema registra o bloqueio e o considera indisponível no período correspondente.

2. Dado que um Solicitante tenta gerenciar bloqueios,
   Quando solicita a operação,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de bloqueios aplicados à disponibilidade
- **Definição:** Percentual de bloqueios registrados que impedem reservas no período correspondente
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada bloqueio criado por Administrador para recurso e período definido
- **Método de validação:** Testes de integração com Testcontainers: criar bloqueio, tentar reservar no período, verificar recusa
- **Critério de aprovação:** 100% dos bloqueios impedem reservas; recursos bloqueados não aparecem como disponíveis

### RF-07: Gestão de manutenção

- **Descrição:** O sistema deve permitir ao Administrador gerenciar períodos de manutenção de recursos.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E6: Manutenção e Bloqueios.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Requisito oficial relacionado:** 8. Bloqueio de recursos em manutenção.
- **Regras de negócio relacionadas:** RN-05.
- **Pré-condições:** Administrador autenticado e recurso cadastrado.
- **Resultado esperado:** período de manutenção registrado e aplicado à disponibilidade do recurso.
- **Evidência esperada:** testes de integração com banco em Testcontainers e testes de API.

#### Critérios de aceitação

1. Dado que o Administrador está autenticado e o recurso existe,
   Quando registra um período de manutenção,
   Então o sistema bloqueia reservas do recurso nesse período.

2. Dado que um Solicitante tenta reservar o recurso durante a manutenção,
   Quando envia a solicitação,
   Então o sistema recusa a reserva e informa a indisponibilidade.

#### Métrica funcional

- **Nome:** Taxa de períodos de manutenção aplicados à indisponibilidade
- **Definição:** Percentual de períodos de manutenção que impedem reservas no intervalo correspondente
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada período de manutenção registrado por Administrador
- **Método de validação:** Testes de integração com Testcontainers: registrar manutenção, tentar reservar no período, verificar recusa
- **Critério de aprovação:** 100% dos períodos de manutenção impedem reservas; recursos em manutenção não aparecem como disponíveis

### RF-08: Consulta de recursos

- **Descrição:** O sistema deve permitir ao Solicitante consultar salas, professores e materiais disponíveis no cadastro.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Seção de origem:** Responsabilidades, Permissões e Funcionalidades Utilizadas.
- **Escopo principal:** E3: Pesquisa e Disponibilidade.
- **Escopos relacionados:** E2: Cadastro de Recursos.
- **Requisito oficial relacionado:** 2. Cadastro e consulta de salas, professores e materiais.
- **Regras de negócio relacionadas:** RN-05.
- **Pré-condições:** Solicitante autenticado; recursos cadastrados.
- **Resultado esperado:** recursos cadastrados podem ser consultados sem permitir gestão não autorizada.
- **Evidência esperada:** testes de API e end-to-end com consulta autorizada e não autorizada.

#### Critérios de aceitação

1. Dado que o Solicitante está autenticado,
   Quando consulta salas, professores ou materiais,
   Então o sistema retorna os recursos cadastrados para consulta.

2. Dado que o Solicitante consulta um recurso em manutenção,
   Quando verifica sua disponibilidade,
   Então o sistema informa que o recurso não pode ser reservado no período de manutenção.

#### Métrica funcional

- **Nome:** Taxa de consultas retornando recursos disponíveis corretos
- **Definição:** Percentual de consultas que retornam somente recursos livres, não bloqueados e fora de manutenção
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada consulta realizada por Solicitante autenticado
- **Método de validação:** Testes de API com recursos em vários estados (livre, reservado, bloqueado, manutenção)
- **Critério de aprovação:** 100% das consultas retornam dados corretos; recursos indisponíveis não são listados

### RF-09: Pesquisa por filtros e disponibilidade

- **Descrição:** O sistema deve permitir pesquisar recursos por tipo, capacidade, localização, competência e disponibilidade.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Seção de origem:** Objetivo Principal, Responsabilidades e Funcionalidades Utilizadas.
- **Escopo principal:** E3: Pesquisa e Disponibilidade.
- **Escopos relacionados:** E4: Reservas e Agenda; E6: Manutenção e Bloqueios.
- **Requisito oficial relacionado:** 3. Pesquisa por tipo, capacidade, localização, competência e disponibilidade.
- **Regras de negócio relacionadas:** RN-02, RN-03, RN-05.
- **Pré-condições:** Solicitante autenticado; recursos cadastrados e agenda disponível para consulta.
- **Resultado esperado:** a pesquisa retorna somente recursos compatíveis com os filtros e o período informado.
- **Evidência esperada:** testes parametrizados de API e end-to-end para cada filtro e para recursos indisponíveis.

#### Critérios de aceitação

1. Dado que existem recursos cadastrados com diferentes tipos, capacidades, localizações, competências e agendas,
   Quando o Solicitante pesquisa usando esses filtros,
   Então o sistema retorna os recursos compatíveis com os filtros informados.

2. Dado que um recurso está reservado, bloqueado, em manutenção ou conflita com a agenda do professor no período,
   Quando o Solicitante pesquisa sua disponibilidade,
   Então o sistema não o apresenta como disponível para reserva naquele período.

#### Métrica funcional

- **Nome:** Taxa de pesquisas retornando recursos aplicando filtros e disponibilidade
- **Definição:** Percentual de pesquisas que retornam somente recursos compatíveis com filtros e disponíveis no período
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada pesquisa com tipo, capacidade, localização, competência e período
- **Método de validação:** Testes parametrizados de API com cada filtro e combinações; recursos indisponíveis testados
- **Critério de aprovação:** 100% das pesquisas retornam resultados corretos conforme filtros; zero recursos falsos positivos

### RF-10: Criação de reservas

- **Descrição:** O sistema deve permitir ao Solicitante criar reservas de salas, professores e materiais para períodos válidos.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Seção de origem:** Responsabilidades, Permissões, Restrições e Critérios de Sucesso.
- **Escopo principal:** E4: Reservas e Agenda.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E5: Aprovação de Recursos Restritos; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 4. Criação, alteração e cancelamento de reservas.
- **Regras de negócio relacionadas:** RN-01, RN-02, RN-03, RN-04, RN-05, RN-06, RN-07.
- **Pré-condições:** Solicitante autenticado; recursos cadastrados; término posterior ao início; recursos livres e fora de manutenção.
- **Resultado esperado:** uma solicitação de reserva é registrada sem conflito; se o recurso for restrito, segue o fluxo de aprovação.
- **Evidência esperada:** testes unitários, parametrizados, integração, API, end-to-end e concorrência automatizada.

#### Critérios de aceitação

1. Dado que o Solicitante está autenticado e os recursos estão disponíveis,
   Quando cria uma reserva com término posterior ao início,
   Então o sistema registra a solicitação sem sobreposição de sala, material ou professor.

2. Dado que o período é inválido, há sobreposição, manutenção ou recurso restrito sem aprovação,
   Quando o Solicitante cria a reserva,
   Então o sistema recusa ou mantém a solicitação no estado aplicável e informa o motivo observável.

3. Dado que dois Solicitantes enviam simultaneamente o mesmo recurso e período,
   Quando as solicitações são processadas,
   Então somente uma reserva é aceita.

#### Métrica funcional

- **Nome:** Taxa de reservas criadas sem sobreposição e com única aceita em dupla
- **Definição:** Percentual de reservas criadas que não conflitam com sala, material, professor e que em cenário concorrente resultam em apenas uma aceita
- **Valor-alvo:** 100% sem conflito; 1 reserva aceita em dupla simultânea
- **Unidade:** Percentual (conflitos); quantidade (dupla)
- **Condição de medição:** Cada criação com período válido, recursos livres e fora de manutenção; duas solicitações simultâneas para mesmo recurso e período
- **Método de validação:** Testes unitários, parametrizados, integração, API, E2E e concorrência com Testcontainers
- **Critério de aprovação:** 100% de reservas sem conflito; exatamente 1 reserva aceita em dupla; recurso restrito segue para aprovação

### RF-11: Alteração de reservas

- **Descrição:** O sistema deve permitir ao Solicitante alterar suas próprias reservas quando a alteração respeitar as regras de período, conflito e manutenção.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Seção de origem:** Responsabilidades, Permissões, Restrições e Regras de Negócio Relacionadas.
- **Escopo principal:** E4: Reservas e Agenda.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E5: Aprovação de Recursos Restritos; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 4. Criação, alteração e cancelamento de reservas.
- **Regras de negócio relacionadas:** RN-01, RN-02, RN-03, RN-05, RN-06, RN-09.
- **Pré-condições:** Solicitante autenticado; reserva pertence ao Solicitante; reserva não está iniciada; novos dados são válidos.
- **Resultado esperado:** reserva alterada sem conflito e mudança de estado registrada em auditoria quando aplicável.
- **Evidência esperada:** testes de API, integração, autorização, validação de entrada e auditoria.

#### Critérios de aceitação

1. Dado que a reserva pertence ao Solicitante, não foi iniciada e o novo período está livre,
   Quando o Solicitante altera a reserva,
   Então o sistema salva a alteração sem conflito.

2. Dado que a reserva pertence a outro Solicitante, já foi iniciada, conflita ou usa recurso em manutenção,
   Quando o Solicitante tenta alterá-la,
   Então o sistema recusa a operação.

3. Dado que a alteração muda o estado da reserva,
   Quando a alteração é concluída,
   Então o sistema gera registro de auditoria.

#### Métrica funcional

- **Nome:** Taxa de alterações aplicadas corretamente com auditoria
- **Definição:** Percentual de alterações de reserva que são aceitas sem conflito e geram auditoria quando mérito
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada alteração de reserva própria não iniciada com dados válidos
- **Método de validação:** Testes de API, autorização, validação e auditoria com Testcontainers
- **Critério de aprovação:** 100% das alterações permitidas são aplicadas; alterações proibidas são recusadas; mudanças de estado geram auditoria

### RF-12: Cancelamento de reservas

- **Descrição:** O sistema deve permitir ao Solicitante cancelar suas próprias reservas quando o cancelamento não violar a regra de reserva iniciada.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Seção de origem:** Responsabilidades, Permissões, Restrições e Regras de Negócio Relacionadas.
- **Escopo principal:** E4: Reservas e Agenda.
- **Escopos relacionados:** E8: Auditoria e Histórico; E9: Notificações e Integrações.
- **Requisito oficial relacionado:** 4. Criação, alteração e cancelamento de reservas.
- **Regras de negócio relacionadas:** RN-07, RN-08, RN-09.
- **Pré-condições:** Solicitante autenticado; reserva pertence ao Solicitante; reserva não foi iniciada.
- **Resultado esperado:** reserva passa ao estado `CANCELADA` quando o cancelamento é permitido.
- **Evidência esperada:** testes de API, autorização e auditoria.

#### Critérios de aceitação

1. Dado que a reserva pertence ao Solicitante e ainda não foi iniciada,
   Quando o Solicitante a cancela,
   Então o sistema altera a reserva para `CANCELADA` e registra a mudança.

2. Dado que a reserva já foi iniciada ou pertence a outro Solicitante,
   Quando o usuário tenta cancelá-la,
   Então o sistema recusa a operação e informa o motivo.

#### Métrica funcional

- **Nome:** Taxa de cancelamentos aplicados corretamente com transição e auditoria
- **Definição:** Percentual de cancelamentos de reserva própria não iniciada que são processados e geram transição para CANCELADA com auditoria
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada cancelamento de reserva própria permitido; tentativas de cancelar reserva de terceiro ou iniciada
- **Método de validação:** Testes de API, autorização, transição de estado e auditoria com Testcontainers
- **Critério de aprovação:** 100% dos cancelamentos permitidos são processados com estado CANCELADA; cancelamentos proibidos são recusados; auditoria gerada

### RF-13: Detecção de sobreposição e dupla reserva

- **Descrição:** O sistema deve detectar sobreposição de horários em sala, material e professor e impedir dupla reserva em solicitações simultâneas.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante e Administrador.
- **Arquivo de origem:** `docs/personas/solicitante.md`, `docs/personas/administrador.md`.
- **Seção de origem:** Restrições e Regras de Negócio Relacionadas.
- **Escopo principal:** E4: Reservas e Agenda.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E13: Qualidade, Segurança, Desempenho e CI.
- **Requisito oficial relacionado:** 5. Detecção de sobreposição; 6. Proteção contra dupla reserva em solicitações simultâneas.
- **Regras de negócio relacionadas:** RN-02, RN-03, RN-04.
- **Pré-condições:** solicitações possuem recursos e intervalos de tempo.
- **Resultado esperado:** conflito é identificado e somente uma solicitação simultânea para o mesmo recurso e período é aceita.
- **Evidência esperada:** testes parametrizados para limites de intervalo e teste automatizado de concorrência com Testcontainers.

#### Critérios de aceitação

1. Dado que uma reserva existente usa a mesma sala, material ou professor em período sobreposto,
   Quando uma nova solicitação é enviada,
   Então o sistema recusa a nova reserva e informa o conflito.

2. Dado que duas solicitações simultâneas usam o mesmo recurso e período,
   Quando ambas são processadas,
   Então somente uma resulta em reserva aceita e a outra recebe resultado de conflito.

#### Métrica funcional

- **Nome:** Taxa de detecção de sobreposição e dupla reserva
- **Definição:** Percentual de conflitos detectados (sobreposição em sala, material, professor e dupla simultânea) que são impedidos
- **Valor-alvo:** 100% de conflitos recusados; 1 reserva aceita em dupla
- **Unidade:** Percentual (detecção); quantidade (dupla)
- **Condição de medição:** Cada tentativa de reserva com sobreposição em sala, material ou professor; duas solicitações simultâneas
- **Método de validação:** Testes parametrizados com limites de intervalo; teste concorrência com Testcontainers
- **Critério de aprovação:** 100% dos conflitos detectados são recusados; exatamente 1 reserva aceita em dupla; base de dados consistente

### RF-14: Aprovação de solicitações especiais

- **Descrição:** O sistema deve permitir ao Responsável aprovar ou rejeitar solicitações especiais de recursos restritos.
- **Prioridade:** MUST.
- **Persona de origem:** Responsável.
- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Seção de origem:** Visão Geral, Responsabilidades, Permissões e Regras de Negócio Relacionadas.
- **Escopo principal:** E5: Aprovação de Recursos Restritos.
- **Escopos relacionados:** E4: Reservas e Agenda; E8: Auditoria e Histórico; E9: Notificações e Integrações.
- **Requisito oficial relacionado:** 7. Aprovação obrigatória para recursos restritos.
- **Regras de negócio relacionadas:** RN-06, RN-07, RN-09.
- **Pré-condições:** Responsável autenticado; solicitação especial pendente.
- **Resultado esperado:** solicitação passa a `APROVADA` ou `REJEITADA` conforme a decisão do Responsável.
- **Evidência esperada:** testes positivos e negativos de autorização, API, integração e auditoria.

#### Critérios de aceitação

1. Dado que há solicitação especial pendente e o usuário é Responsável,
   Quando aprova a solicitação,
   Então o sistema altera o estado para `APROVADA` e registra a mudança de estado.

2. Dado que o usuário é Solicitante ou Administrador,
   Quando tenta aprovar recurso restrito,
   Então o sistema recusa a operação.

3. Dado que o Responsável rejeita uma solicitação especial,
   Quando confirma a decisão,
   Então o sistema altera o estado para `REJEITADA` e registra a mudança.

#### Métrica funcional

- **Nome:** Taxa de aprovações/rejeições processadas corretamente com auditoria
- **Definição:** Percentual de solicitações especiais que são aprovadas ou rejeitadas por Responsável autorizado com transição de estado e auditoria
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada solicitação especial pendente; aprovações por Responsável autorizado; rejeições
- **Método de validação:** Testes de autorização, API, integração e auditoria com Testcontainers
- **Critério de aprovação:** 100% das solicitações são processadas; somente Responsável autorizado aprova; estados APROVADA/REJEITADA gerados; auditoria registrada

### RF-15: Validação da alocação de docentes

- **Descrição:** O sistema deve permitir ao Responsável validar a alocação de docentes.
- **Prioridade:** MUST.
- **Persona de origem:** Responsável.
- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Seção de origem:** Responsabilidades, Permissões e Critérios de Sucesso.
- **Escopo principal:** E5: Aprovação de Recursos Restritos.
- **Escopos relacionados:** E4: Reservas e Agenda.
- **Requisito oficial relacionado:** 2. Cadastro e consulta de professores; 5. Detecção de sobreposição na agenda do professor.
- **Regras de negócio relacionadas:** RN-03, RN-07.
- **Pré-condições:** Responsável autenticado; alocação de docente registrada.
- **Resultado esperado:** alocação é validada ou não validada conforme a verificação realizada pelo Responsável.
- **Evidência esperada:** testes de autorização, API e integração com agenda do professor.

#### Critérios de aceitação

1. Dado que o Responsável está autenticado e existe uma alocação de docente,
   Quando executa a validação,
   Então o sistema registra o resultado da validação.

2. Dado que a alocação conflita com a agenda do professor,
   Quando o Responsável tenta validá-la,
   Então o sistema informa o conflito e não a considera validada.

#### Métrica funcional

- **Nome:** Taxa de alocações de docentes validadas sem conflito
- **Definição:** Percentual de alocações de docentes que são validadas pelo Responsável sem conflito na agenda
- **Valor-alvo:** 100% (das permitidas); 0% com conflito aceito
- **Unidade:** Percentual
- **Condição de medição:** Cada alocação de docente registrada; agenda do professor consultada
- **Método de validação:** Testes de autorização, API e integração com agenda docente
- **Critério de aprovação:** 100% das alocações são validadas; conflito na agenda impede validação; zero conflitos aceitos

### RF-16: Registro de retirada de materiais

- **Descrição:** O sistema deve permitir ao Responsável acompanhar e registrar a retirada de materiais e equipamentos.
- **Prioridade:** MUST.
- **Persona de origem:** Responsável.
- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Seção de origem:** Responsabilidades, Permissões, Funcionalidades Utilizadas e Critérios de Sucesso.
- **Escopo principal:** E7: Retirada e Devolução de Materiais.
- **Escopos relacionados:** E4: Reservas e Agenda; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 9. Registro de retirada e devolução de materiais e equipamentos.
- **Regras de negócio relacionadas:** RN-09.
- **Pré-condições:** Responsável autenticado; material ou equipamento associado a uma reserva.
- **Resultado esperado:** retirada fica registrada e disponível para acompanhamento.
- **Evidência esperada:** teste de integração com persistência realista e teste de API de autorização.

#### Critérios de aceitação

1. Dado que o Responsável está autenticado e existe material associado a uma reserva,
   Quando registra a retirada,
   Então o sistema grava a retirada e permite seu acompanhamento.

2. Dado que o Solicitante não possui permissão para registrar retirada,
   Quando tenta executar a operação,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de retiradas registradas e acompanháveis
- **Definição:** Percentual de retiradas de materiais registradas pelo Responsável que são persistidas e recuperáveis
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada material associado a uma reserva registrado para retirada por Responsável
- **Método de validação:** Testes de integração com Testcontainers (persistência realista) e API de autorização
- **Critério de aprovação:** 100% das retiradas permitidas são registradas; somente Responsável registra; operações proibidas são recusadas

### RF-17: Registro de devolução de materiais

- **Descrição:** O sistema deve permitir ao Responsável acompanhar e registrar a devolução de materiais e equipamentos.
- **Prioridade:** MUST.
- **Persona de origem:** Responsável.
- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Seção de origem:** Responsabilidades, Permissões, Funcionalidades Utilizadas e Critérios de Sucesso.
- **Escopo principal:** E7: Retirada e Devolução de Materiais.
- **Escopos relacionados:** E4: Reservas e Agenda; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 9. Registro de retirada e devolução de materiais e equipamentos.
- **Regras de negócio relacionadas:** RN-09.
- **Pré-condições:** Responsável autenticado; retirada registrada.
- **Resultado esperado:** devolução fica registrada e associada à retirada correspondente.
- **Evidência esperada:** teste de integração com persistência realista e teste de API de autorização.

#### Critérios de aceitação

1. Dado que existe uma retirada registrada e o Responsável está autenticado,
   Quando registra a devolução,
   Então o sistema grava a devolução e permite seu acompanhamento.

2. Dado que não existe retirada correspondente,
   Quando o Responsável tenta registrar a devolução,
   Então o sistema recusa a operação e apresenta uma mensagem de erro compreensível.

#### Métrica funcional

- **Nome:** Taxa de devoluções registradas e associadas a retirada
- **Definição:** Percentual de devoluções de materiais registradas pelo Responsável que são associadas a retirada correspondente
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada retirada registrada; devolução correspondente; tentativa de devolução sem retirada
- **Método de validação:** Testes de integração com Testcontainers (persistência realista) e API de autorização
- **Critério de aprovação:** 100% das devoluções são registradas; todas associadas a retirada; devolução sem retirada é recusada

### RF-18: Gestão dos estados da reserva

- **Descrição:** O sistema deve representar o fluxo principal `SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA` e os estados alternativos `REJEITADA`, `CANCELADA` e `NAO_COMPARECEU`.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante e Responsável.
- **Arquivo de origem:** `docs/personas/solicitante.md`, `docs/personas/responsavel.md`.
- **Seção de origem:** Regras de Negócio Relacionadas e Critérios de Sucesso.
- **Escopo principal:** E4: Reservas e Agenda.
- **Escopos relacionados:** E5: Aprovação de Recursos Restritos; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 4. Criação, alteração e cancelamento de reservas.
- **Regras de negócio relacionadas:** RN-06, RN-07, RN-08, RN-09.
- **Pré-condições:** reserva existente e operação autorizada para o estado atual.
- **Resultado esperado:** o sistema mantém a reserva em um estado oficial e rejeita estado não especificado.
- **Evidência esperada:** testes de API e end-to-end dos estados oficiais e de transição não especificada.

#### Critérios de aceitação

1. Dado que uma reserva foi solicitada e aprovada conforme as regras,
   Quando avança pelo fluxo principal,
   Então o sistema representa os estados oficiais na ordem especificada.

2. Dado que uma operação tenta apagar reserva iniciada ou criar estado não oficial,
   Quando é processada,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de transições de estado seguindo fluxo oficial
- **Definição:** Percentual de mudanças de estado que seguem o fluxo oficial (SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA; alternativas REJEITADA, CANCELADA, NAO_COMPARECEU)
- **Valor-alvo:** 100% correto; 0% transições inválidas aceitas
- **Unidade:** Percentual
- **Condição de medição:** Cada mudança de estado; tentativas de estado não oficial; tentativas de apagar reserva iniciada
- **Método de validação:** Testes de API e E2E dos estados e transições; testes de negação de estado inválido
- **Critério de aprovação:** 100% das transições válidas são processadas; estados não oficiais são recusados; reserva iniciada não é apagada

### RF-19: Histórico auditável

- **Descrição:** O sistema deve registrar e permitir consultar o histórico auditável das mudanças de estado das reservas.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante, Responsável e Administrador.
- **Arquivo de origem:** `docs/personas/solicitante.md`, `docs/personas/responsavel.md`, `docs/personas/administrador.md`.
- **Seção de origem:** Regras de Negócio Relacionadas, Permissões e Critérios de Sucesso.
- **Escopo principal:** E8: Auditoria e Histórico.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos; E7: Retirada e Devolução de Materiais.
- **Requisito oficial relacionado:** 10. Histórico auditável de mudanças.
- **Regras de negócio relacionadas:** RN-09, RN-10.
- **Pré-condições:** mudança de estado ou operação auditável realizada por usuário autorizado.
- **Resultado esperado:** registro de auditoria é criado e pode ser consultado pelo perfil autorizado.
- **Evidência esperada:** teste de integração com Testcontainers e consulta de histórico após mudanças.

#### Critérios de aceitação

1. Dado que uma mudança de estado é realizada,
   Quando a mudança é concluída,
   Então o sistema cria um registro de auditoria consultável.

2. Dado que uma reserva possui mudanças de estado,
   Quando o Administrador consulta seu histórico,
   Então o sistema apresenta os registros auditáveis correspondentes.

#### Métrica funcional

- **Nome:** Taxa de mudanças de estado gerando registros auditáveis
- **Definição:** Percentual de mudanças de estado que geram registro de auditoria consultável
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada mudança de estado de reserva; consulta de histórico
- **Método de validação:** Testes de integração com Testcontainers e consulta de histórico após mudanças
- **Critério de aprovação:** 100% das mudanças geram auditoria; histórico é consultável; dados de auditoria persistíam

### RF-20: Notificação ou integração externa

- **Descrição:** O sistema deve produzir uma notificação simulada ou realizar integração com uma API externa relacionada ao fluxo de reservas.
- **Prioridade:** MUST.
- **Persona de origem:** Transversal.
- **Arquivo de origem:** Requisito oficial 11 e escopo E9.
- **Seção de origem:** Requisitos funcionais oficiais mínimos.
- **Escopo principal:** E9: Notificações e Integrações.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos.
- **Requisito oficial relacionado:** 11. Notificação simulada ou integração com API externa.
- **Regras de negócio relacionadas:** RN-06, RN-07, RN-09.
- **Pré-condições:** evento do fluxo de reserva definido e mecanismo de notificação ou integração disponível para validação.
- **Resultado esperado:** a notificação simulada ou chamada externa é produzida para o evento implementado.
- **Evidência esperada:** teste de integração com WireMock ou evidência da notificação simulada.

#### Critérios de aceitação

1. Dado que ocorre um evento do fluxo que utiliza notificação ou integração,
   Quando o evento é concluído,
   Então o sistema produz a notificação simulada ou realiza a chamada externa definida.

2. Dado que a API externa não responde,
   Quando a integração é acionada,
   Então o sistema registra o resultado da falha de forma segura e observável.

#### Métrica funcional

- **Nome:** Taxa de notificações ou chamadas externas produzidas e falhas registradas
- **Definição:** Percentual de eventos do fluxo que acionam notificação simulada ou integração com API externa com sucesso; falhas registradas de forma segura
- **Valor-alvo:** 100% de eventos processados; falhas registradas sem expor detalhes internos
- **Unidade:** Percentual
- **Condição de medição:** Cada evento do fluxo que utiliza notificação; integração disponível e indisponível
- **Método de validação:** Testes de integração com WireMock ou notificação simulada
- **Critério de aprovação:** 100% dos eventos produzem notificação; falhas são registradas; nenhuma exposição de detalhes internos

### RF-21: Relatórios operacionais

- **Descrição:** O sistema deve disponibilizar relatório de utilização por recurso, carga horária alocada e conflitos evitados.
- **Prioridade:** MUST.
- **Persona de origem:** Administrador.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Seção de origem:** Funcionalidades Utilizadas, Permissões e Critérios de Sucesso.
- **Escopo principal:** E10: Relatórios.
- **Escopos relacionados:** E4: Reservas e Agenda; E8: Auditoria e Histórico.
- **Requisito oficial relacionado:** 12. Relatório de utilização por recurso, carga horária alocada e conflitos evitados.
- **Regras de negócio relacionadas:** RN-02, RN-03, RN-04, RN-10.
- **Pré-condições:** Administrador autenticado; dados de reservas e conflitos registrados.
- **Resultado esperado:** relatório apresenta os três indicadores solicitados por recurso ou período consultado.
- **Evidência esperada:** testes de API, integração e end-to-end com dados controlados.

#### Critérios de aceitação

1. Dado que existem reservas e registros de conflito,
   Quando o Administrador consulta o relatório,
   Então o sistema apresenta utilização por recurso, carga horária alocada e conflitos evitados.

2. Dado que um Solicitante não possui permissão para consultar relatórios operacionais,
   Quando tenta acessá-los,
   Então o sistema recusa a operação.

#### Métrica funcional

- **Nome:** Taxa de relatórios apresentando utilização, carga horária e conflitos evitados
- **Definição:** Percentual de relatórios consultados que apresentam os três indicadores (utilização por recurso, carga horária alocada, conflitos evitados) com dados consistentes
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada consulta de relatório por Administrador; dados de reservas e conflitos registrados
- **Método de validação:** Testes de API, integração e E2E com dados controlados
- **Critério de aprovação:** 100% dos relatórios apresentam os três indicadores; somente Administrador consulta; dados são consistentes

### RF-22: Interface responsiva e erros compreensíveis

- **Descrição:** O sistema deve apresentar interface responsiva e mensagens de erro compreensíveis nos fluxos públicos do sistema.
- **Prioridade:** MUST.
- **Persona de origem:** Solicitante, Responsável e Administrador.
- **Arquivo de origem:** Requisito oficial 13 e arquivos das três personas.
- **Seção de origem:** Requisitos funcionais oficiais mínimos; Restrições e Critérios de Sucesso.
- **Escopo principal:** E11: Interface, Erros e Acessibilidade.
- **Escopos relacionados:** E1: Acesso e Perfis; E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Requisito oficial relacionado:** 13. Interface responsiva e mensagens de erro compreensíveis.
- **Regras de negócio relacionadas:** RN-01, RN-02, RN-05, RN-06, RN-08.
- **Pré-condições:** usuário acessa um fluxo do sistema em dispositivo ou viewport suportado; ocorre operação válida ou erro conhecido.
- **Resultado esperado:** conteúdo se adapta à viewport e erros informam o motivo da recusa sem expor detalhes inseguros.
- **Evidência esperada:** testes end-to-end em viewports definidos pela equipe e testes de validação de entradas e erros seguros.

#### Critérios de aceitação

1. Dado que uma persona acessa um fluxo público em uma viewport suportada,
   Quando utiliza a interface,
   Então os controles e mensagens permanecem utilizáveis sem sobreposição de conteúdo.

2. Dado que ocorre período inválido, conflito, manutenção ou falta de autorização,
   Quando a operação é recusada,
   Então o sistema apresenta mensagem compreensível e não expõe informação sensível.

#### Métrica funcional

- **Nome:** Taxa de fluxos públicos com interface utilizável e erros compreensíveis
- **Definição:** Percentual de fluxos públicos onde interface é responsiva sem sobreposição e erros informam causa observável
- **Valor-alvo:** 100%
- **Unidade:** Percentual
- **Condição de medição:** Cada fluxo público em viewport suportada; operação válida e inválida (erro)
- **Método de validação:** Testes E2E em viewports definidos pela equipe; testes de validação de entrada e erros seguros
- **Critério de aprovação:** 100% dos fluxos são utilizáveis sem sobreposição; erros informam motivo sem expor detalhes internos

### RF-23: Documentação da API ou dos fluxos públicos

- **Descrição:** O sistema deve disponibilizar documentação da API ou dos fluxos públicos do sistema.
- **Prioridade:** MUST.
- **Persona de origem:** Transversal.
- **Arquivo de origem:** Requisito oficial 14 e escopo E12.
- **Seção de origem:** Requisitos funcionais oficiais mínimos.
- **Escopo principal:** E12: Documentação da API ou Fluxos Públicos.
- **Escopos relacionados:** E1: Acesso e Perfis; E4: Reservas e Agenda; E9: Notificações e Integrações.
- **Requisito oficial relacionado:** 14. Documentação da API ou dos fluxos públicos do sistema.
- **Regras de negócio relacionadas:** RN-06, RN-07, RN-09.
- **Pré-condições:** API ou fluxos públicos definidos.
- **Resultado esperado:** documentação acessível descreve os fluxos ou contratos públicos existentes.
- **Evidência esperada:** inspeção documental e verificação de que os fluxos públicos estão descritos.

#### Critérios de aceitação

1. Dado que os fluxos públicos ou a API estão definidos,
   Quando a documentação é consultada,
   Então ela descreve os fluxos ou contratos disponibilizados pelo sistema.

2. Dado que um fluxo público possui estados, autorização ou erros relevantes,
   Quando é documentado,
   Então essas condições observáveis estão incluídas na documentação.

## 8. Requisitos Não Funcionais

### RNF-01: Plataforma de execução

- **Descrição mensurável:** O sistema deve ser executável em Java 21 e Spring Boot 3.x.
- **Categoria:** manutenibilidade.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Contexto oficial do projeto.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E12: Documentação da API ou Fluxos Públicos.
- **Métrica:** versão da plataforma e framework.
- **Valor-alvo:** Java 21 e Spring Boot 3.x.
- **Unidade:** versão.
- **Condição de medição:** inspeção do build e execução do sistema.
- **Método ou ferramenta de validação:** inspeção de configuração e pipeline de build.
- **Critério de aprovação:** a aplicação compila e executa usando as versões oficiais.
- **Evidência esperada:** configuração de build e log de execução do pipeline.

### RNF-02: Cobertura de linhas

- **Descrição mensurável:** O conjunto de testes deve atingir no mínimo 80% de cobertura de linhas.
- **Categoria:** cobertura.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda; E8: Auditoria e Histórico.
- **Métrica:** cobertura de linhas.
- **Valor-alvo:** mínimo de 80%.
- **Unidade:** percentual.
- **Condição de medição:** execução da suíte de testes definida no pipeline.
- **Método ou ferramenta de validação:** JaCoCo.
- **Critério de aprovação:** relatório JaCoCo indica pelo menos 80% de linhas cobertas.
- **Evidência esperada:** relatório JaCoCo anexado à execução de qualidade.

### RNF-03: Cobertura de branches

- **Descrição mensurável:** O conjunto de testes deve atingir no mínimo 70% de cobertura de branches.
- **Categoria:** cobertura.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos.
- **Métrica:** cobertura de branches.
- **Valor-alvo:** mínimo de 70%.
- **Unidade:** percentual.
- **Condição de medição:** execução da suíte de testes definida no pipeline.
- **Método ou ferramenta de validação:** JaCoCo.
- **Critério de aprovação:** relatório JaCoCo indica pelo menos 70% de branches cobertos.
- **Evidência esperada:** relatório JaCoCo anexado à execução de qualidade.

### RNF-04: Rastreabilidade de requisitos críticos

- **Descrição mensurável:** Todos os requisitos críticos devem possuir rastreabilidade completa na matriz do PRD.
- **Categoria:** auditabilidade.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E8: Auditoria e Histórico.
- **Métrica:** requisitos críticos rastreados.
- **Valor-alvo:** 100%.
- **Unidade:** percentual.
- **Condição de medição:** revisão da matriz de rastreabilidade contra a baseline.
- **Método ou ferramenta de validação:** revisão documental pelo Analyst, Product Manager, QA e Architect.
- **Critério de aprovação:** 100% dos requisitos críticos possuem origem, escopo, regra e evidência.
- **Evidência esperada:** matriz de rastreabilidade revisada.

### RNF-05: Bugs críticos conhecidos

- **Descrição mensurável:** A entrega não deve possuir bugs críticos conhecidos.
- **Categoria:** qualidade de código.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos.
- **Métrica:** quantidade de bugs críticos conhecidos.
- **Valor-alvo:** zero.
- **Unidade:** quantidade.
- **Condição de medição:** fechamento da avaliação de qualidade da entrega.
- **Método ou ferramenta de validação:** revisão de QA e resultados dos testes.
- **Critério de aprovação:** nenhum bug classificado como crítico permanece conhecido.
- **Evidência esperada:** relatório de QA sem bug crítico conhecido.

### RNF-06: Vulnerabilidades críticas conhecidas

- **Descrição mensurável:** A entrega não deve possuir vulnerabilidades críticas conhecidas.
- **Categoria:** segurança.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E1: Acesso e Perfis; E8: Auditoria e Histórico.
- **Métrica:** quantidade de vulnerabilidades críticas conhecidas.
- **Valor-alvo:** zero.
- **Unidade:** quantidade.
- **Condição de medição:** análise de segurança da entrega.
- **Método ou ferramenta de validação:** análise estática com SonarCloud e testes de autenticação, autorização, entrada e erros seguros.
- **Critério de aprovação:** nenhuma vulnerabilidade classificada como crítica permanece conhecida.
- **Evidência esperada:** resultado de SonarCloud e relatório de segurança.

### RNF-07: Validação automatizada de persistência crítica

- **Descrição mensurável:** A persistência crítica de reservas, estados, auditoria e movimentação de materiais deve ser validada em banco de dados containerizado, sem depender apenas de mocks.
- **Categoria:** testabilidade.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante, Responsável e Administrador.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade e regras críticas.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda; E7: Retirada e Devolução de Materiais; E8: Auditoria e Histórico.
- **Métrica:** existência de testes de integração com persistência realista para cada área crítica.
- **Valor-alvo:** todas as áreas críticas cobertas; valor numérico adicional pendente de aprovação da equipe.
- **Unidade:** áreas funcionais cobertas.
- **Condição de medição:** execução dos testes de integração.
- **Método ou ferramenta de validação:** Testcontainers.
- **Critério de aprovação:** os testes críticos executam contra banco containerizado e não somente mocks.
- **Evidência esperada:** logs e resultados dos testes com Testcontainers.

### RNF-08: Validação de integrações externas

- **Descrição mensurável:** Integrações externas devem ser verificadas em ambiente simulado com WireMock ou em integração disponível, conforme a alternativa adotada.
- **Categoria:** integração.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade e requisito oficial 11.
- **Escopo principal:** E9: Notificações e Integrações.
- **Escopos relacionados:** E13: Qualidade, Segurança, Desempenho e CI.
- **Métrica:** integração externa do fluxo de notificação validada.
- **Valor-alvo:** validação executada; quantidade e contrato da integração real pendentes de aprovação da equipe.
- **Unidade:** integração.
- **Condição de medição:** execução do teste do fluxo de notificação ou integração.
- **Método ou ferramenta de validação:** WireMock quando a integração for externa.
- **Critério de aprovação:** o teste comprova a solicitação esperada e trata a falha sem erro inseguro.
- **Evidência esperada:** relatório de teste WireMock ou evidência da integração.

### RNF-09: Testes de concorrência

- **Descrição mensurável:** O comportamento de solicitações simultâneas deve ser validado por teste automatizado de concorrência.
- **Categoria:** concorrência.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante e Administrador.
- **Arquivo ou requisito de origem:** Regras críticas de tempo e concorrência e estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda.
- **Métrica:** cenário de dupla reserva simultânea executado.
- **Valor-alvo:** somente uma reserva aceita no cenário definido; quantidade de execuções adicionais pendente de aprovação da equipe.
- **Unidade:** reservas aceitas por cenário.
- **Condição de medição:** duas solicitações simultâneas para o mesmo recurso e período.
- **Método ou ferramenta de validação:** teste automatizado de concorrência com banco em Testcontainers.
- **Critério de aprovação:** o resultado contém somente uma reserva aceita.
- **Evidência esperada:** relatório do teste concorrente.

### RNF-10: Testes automatizados em camadas

- **Descrição mensurável:** A validação deve contemplar testes unitários com JUnit 5, parametrizados, de integração, API em caixa-preta e end-to-end.
- **Categoria:** testabilidade.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos; E8: Auditoria e Histórico.
- **Métrica:** tipos de teste exigidos presentes na evidência.
- **Valor-alvo:** todos os cinco tipos exigidos presentes; quantidade de testes por tipo pendente de aprovação da equipe.
- **Unidade:** tipos de teste.
- **Condição de medição:** revisão da suíte e execução dos testes.
- **Método ou ferramenta de validação:** JUnit 5, testes de API e execução end-to-end.
- **Critério de aprovação:** cada tipo de teste exigido possui evidência de execução.
- **Evidência esperada:** relatórios e logs da suíte.

### RNF-11: TDD ou BDD em funcionalidade nova

- **Descrição mensurável:** Deve existir evidência de TDD ou BDD em pelo menos uma funcionalidade nova.
- **Categoria:** qualidade de código.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E4: Reservas e Agenda.
- **Métrica:** funcionalidades novas com evidência TDD ou BDD.
- **Valor-alvo:** pelo menos uma.
- **Unidade:** funcionalidade.
- **Condição de medição:** revisão dos artefatos de desenvolvimento e testes.
- **Método ou ferramenta de validação:** inspeção de commits, cenários BDD ou sequência de testes TDD.
- **Critério de aprovação:** existe evidência verificável em ao menos uma funcionalidade nova.
- **Evidência esperada:** histórico ou artefatos de TDD/BDD.

### RNF-12: Integração contínua em pull requests

- **Descrição mensurável:** GitHub Actions deve executar as verificações de qualidade em pull requests.
- **Categoria:** integração contínua.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E12: Documentação da API ou Fluxos Públicos.
- **Métrica:** execução do workflow em pull request.
- **Valor-alvo:** execução configurada para pull requests; critérios adicionais de bloqueio pendentes de aprovação da equipe.
- **Unidade:** execução de workflow.
- **Condição de medição:** abertura ou atualização de pull request.
- **Método ou ferramenta de validação:** GitHub Actions.
- **Critério de aprovação:** há execução registrada do workflow no pull request.
- **Evidência esperada:** execução do workflow e seus artefatos.

### RNF-13: Análise estática

- **Descrição mensurável:** O código deve ser submetido à análise estática pelo SonarCloud.
- **Categoria:** qualidade de código.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E1: Acesso e Perfis; E8: Auditoria e Histórico.
- **Métrica:** análise estática executada e vulnerabilidades críticas conhecidas.
- **Valor-alvo:** análise executada e zero vulnerabilidades críticas conhecidas.
- **Unidade:** execução e quantidade.
- **Condição de medição:** pipeline de qualidade da entrega.
- **Método ou ferramenta de validação:** SonarCloud.
- **Critério de aprovação:** análise disponível e sem vulnerabilidade crítica conhecida.
- **Evidência esperada:** resultado do SonarCloud.

### RNF-14: Desempenho sob carga

- **Descrição mensurável:** O comportamento do sistema sob carga deve ser medido com JMeter.
- **Categoria:** desempenho.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante, Responsável e Administrador.
- **Arquivo ou requisito de origem:** Estratégia obrigatória de qualidade.
- **Escopo principal:** E13: Qualidade, Segurança, Desempenho e CI.
- **Escopos relacionados:** E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda; E10: Relatórios.
- **Métrica:** resultados do teste de carga, incluindo tempo de resposta e taxa de erro.
- **Valor-alvo:** pendente de aprovação da equipe.
- **Unidade:** pendente de aprovação da equipe.
- **Condição de medição:** plano de carga definido pela equipe para consultas de disponibilidade, reservas e relatórios.
- **Método ou ferramenta de validação:** JMeter.
- **Critério de aprovação:** cumprir o valor-alvo e a condição de erro aprovados pela equipe.
- **Evidência esperada:** relatório JMeter aprovado pela equipe.

### RNF-15: Segurança de autenticação, autorização, entrada e erros

- **Descrição mensurável:** Os fluxos de autenticação, autorização, validação de entrada e tratamento de erros devem possuir testes positivos e negativos e não devem expor informação sensível em erros.
- **Categoria:** segurança.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante, Responsável e Administrador.
- **Arquivo ou requisito de origem:** Personas, requisitos oficiais 1 e 13 e estratégia obrigatória de qualidade.
- **Escopo principal:** E1: Acesso e Perfis.
- **Escopos relacionados:** E4: Reservas e Agenda; E5: Aprovação de Recursos Restritos; E11: Interface, Erros e Acessibilidade; E13: Qualidade, Segurança, Desempenho e CI.
- **Métrica:** cenários de segurança definidos executados e informações sensíveis expostas em erros.
- **Valor-alvo:** todos os fluxos críticos testados; zero exposição de informação sensível; quantidade exata de cenários pendente de aprovação da equipe.
- **Unidade:** cenários e ocorrências.
- **Condição de medição:** testes positivos e negativos dos perfis e entradas críticas.
- **Método ou ferramenta de validação:** testes de API, end-to-end, análise de SonarCloud e revisão de QA.
- **Critério de aprovação:** autorização negativa é recusada, entradas inválidas são tratadas e erros não expõem informação sensível.
- **Evidência esperada:** resultados de testes e relatório de segurança.

### RNF-16: Responsividade e acessibilidade

- **Descrição mensurável:** A interface deve ser avaliada em viewports definidos pela equipe e os controles e textos não devem se sobrepor ou ficar inacessíveis nesses cenários.
- **Categoria:** responsividade.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante, Responsável e Administrador.
- **Arquivo ou requisito de origem:** Requisito oficial 13 e RF-22.
- **Escopo principal:** E11: Interface, Erros e Acessibilidade.
- **Escopos relacionados:** E1: Acesso e Perfis; E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Métrica:** viewports definidos sem sobreposição ou inacessibilidade observável.
- **Valor-alvo:** todas as viewports definidas pela equipe; lista de viewports e meta adicional pendentes de aprovação.
- **Unidade:** viewport.
- **Condição de medição:** execução dos fluxos públicos em cada viewport aprovada.
- **Método ou ferramenta de validação:** testes end-to-end e inspeção de interface.
- **Critério de aprovação:** todos os fluxos testados permanecem utilizáveis e sem sobreposição.
- **Evidência esperada:** capturas ou relatório de validação nos viewports aprovados.

### RNF-17: Mensagens de erro compreensíveis

- **Descrição mensurável:** Cada erro dos fluxos críticos deve apresentar mensagem que identifique o motivo observável da recusa sem linguagem subjetiva ou informação sensível.
- **Categoria:** usabilidade.
- **Prioridade:** MUST.
- **Personas afetadas:** Solicitante, Responsável e Administrador.
- **Arquivo ou requisito de origem:** Requisito oficial 13 e RF-22.
- **Escopo principal:** E11: Interface, Erros e Acessibilidade.
- **Escopos relacionados:** E1: Acesso e Perfis; E3: Pesquisa e Disponibilidade; E4: Reservas e Agenda.
- **Métrica:** erros críticos com mensagem de causa observável.
- **Valor-alvo:** todos os erros dos fluxos críticos; quantidade exata de fluxos pendente de aprovação da equipe.
- **Unidade:** erro de fluxo.
- **Condição de medição:** execução de entradas inválidas, conflitos, manutenção e falta de autorização.
- **Método ou ferramenta de validação:** testes de API e end-to-end e revisão de QA.
- **Critério de aprovação:** cada erro testado informa causa observável e não expõe informação sensível.
- **Evidência esperada:** resultados dos testes e catálogo de mensagens avaliado.

### RNF-18: Documentação verificável dos fluxos públicos

- **Descrição mensurável:** A documentação deve permitir verificar os fluxos públicos, estados, autorizações e erros definidos para a API ou os fluxos documentados.
- **Categoria:** documentação.
- **Prioridade:** MUST.
- **Personas afetadas:** Transversal.
- **Arquivo ou requisito de origem:** Requisito oficial 14 e RF-23.
- **Escopo principal:** E12: Documentação da API ou Fluxos Públicos.
- **Escopos relacionados:** E1: Acesso e Perfis; E4: Reservas e Agenda; E8: Auditoria e Histórico.
- **Métrica:** itens públicos documentados e verificáveis.
- **Valor-alvo:** todos os itens dos fluxos públicos escolhidos; quantidade exata pendente de aprovação da equipe.
- **Unidade:** item documentado.
- **Condição de medição:** comparação da documentação com a baseline implementada.
- **Método ou ferramenta de validação:** inspeção documental e teste de API ou fluxo descrito.
- **Critério de aprovação:** não há fluxo público escolhido sem sua descrição correspondente.
- **Evidência esperada:** documentação revisada e evidência de verificação.

## 9. Matriz de Rastreabilidade Inicial

| ID | Tipo | Título | Persona | Arquivo de origem | Escopo principal | Requisito oficial | Regra relacionada | Prioridade | Evidência esperada |
|---|---|---|---|---|---|---|---|---|---|
| RF-01 | RF | Autenticação e autorização por perfil | Solicitante; Responsável; Administrador | Personas oficiais | E1 | 1 | RN-06 | MUST | Testes positivos e negativos de autenticação e autorização |
| RF-02 | RF | Gestão de salas | Administrador | administrador.md | E2 | 2 | RN-05 | MUST | Testes de API e integração |
| RF-03 | RF | Gestão de professores | Administrador | administrador.md | E2 | 2 | RN-03 | MUST | Testes de API, integração e agenda |
| RF-04 | RF | Gestão de materiais | Administrador | administrador.md | E2 | 2 | RN-05 | MUST | Testes de API e integração |
| RF-05 | RF | Gestão de usuários | Administrador | administrador.md | E1 | 1 | RN-06 | MUST | Testes de API e autorização |
| RF-06 | RF | Gestão de bloqueios | Administrador | administrador.md | E6 | 8 | RN-05 | MUST | Testes de API e integração |
| RF-07 | RF | Gestão de manutenção | Administrador | administrador.md | E6 | 8 | RN-05 | MUST | Testes de integração e API |
| RF-08 | RF | Consulta de recursos | Solicitante | solicitante.md | E3 | 2 | RN-05 | MUST | Testes de API e end-to-end |
| RF-09 | RF | Pesquisa por filtros e disponibilidade | Solicitante | solicitante.md | E3 | 3 | RN-02; RN-03; RN-05 | MUST | Testes parametrizados e end-to-end |
| RF-10 | RF | Criação de reservas | Solicitante | solicitante.md | E4 | 4 | RN-01; RN-02; RN-03; RN-04; RN-05; RN-06; RN-07 | MUST | Testes unitários, integração, API, E2E e concorrência |
| RF-11 | RF | Alteração de reservas | Solicitante | solicitante.md | E4 | 4 | RN-01; RN-02; RN-03; RN-05; RN-06; RN-09 | MUST | Testes de API, autorização e auditoria |
| RF-12 | RF | Cancelamento de reservas | Solicitante | solicitante.md | E4 | 4 | RN-07; RN-08; RN-09 | MUST | Testes de API, autorização e auditoria |
| RF-13 | RF | Detecção de sobreposição e dupla reserva | Solicitante; Administrador | Personas oficiais | E4 | 5; 6 | RN-02; RN-03; RN-04 | MUST | Testes parametrizados e concorrência |
| RF-14 | RF | Aprovação de solicitações especiais | Responsável | responsavel.md | E5 | 7 | RN-06; RN-07; RN-09 | MUST | Testes de autorização, API, integração e auditoria |
| RF-15 | RF | Validação da alocação de docentes | Responsável | responsavel.md | E5 | 2; 5 | RN-03; RN-07 | MUST | Testes de autorização, API e integração |
| RF-16 | RF | Registro de retirada de materiais | Responsável | responsavel.md | E7 | 9 | RN-09 | MUST | Testes com persistência realista |
| RF-17 | RF | Registro de devolução de materiais | Responsável | responsavel.md | E7 | 9 | RN-09 | MUST | Testes com persistência realista |
| RF-18 | RF | Gestão dos estados da reserva | Solicitante; Responsável | Personas oficiais | E4 | 4 | RN-06; RN-07; RN-08; RN-09 | MUST | Testes de API e end-to-end |
| RF-19 | RF | Histórico auditável | Solicitante; Responsável; Administrador | Personas oficiais | E8 | 10 | RN-09; RN-10 | MUST | Testes de integração e consulta |
| RF-20 | RF | Notificação ou integração externa | Transversal | Requisito oficial 11 | E9 | 11 | RN-06; RN-07; RN-09 | MUST | WireMock ou evidência de notificação simulada |
| RF-21 | RF | Relatórios operacionais | Administrador | administrador.md | E10 | 12 | RN-02; RN-03; RN-04; RN-10 | MUST | Testes de API, integração e E2E |
| RF-22 | RF | Interface responsiva e erros compreensíveis | Solicitante; Responsável; Administrador | Requisito oficial 13 e personas | E11 | 13 | RN-01; RN-02; RN-05; RN-06; RN-08 | MUST | Testes E2E e validação de erros |
| RF-23 | RF | Documentação da API ou dos fluxos públicos | Transversal | Requisito oficial 14 | E12 | 14 | RN-06; RN-07; RN-09 | MUST | Inspeção documental |
| RNF-01 | RNF | Plataforma de execução | Transversal | Contexto oficial | E13 | Tecnologias e contexto | RN-10 | MUST | Configuração e log de build |
| RNF-02 | RNF | Cobertura de linhas | Transversal | Estratégia de qualidade | E13 | Meta de 80% de linhas | RN-10 | MUST | Relatório JaCoCo |
| RNF-03 | RNF | Cobertura de branches | Transversal | Estratégia de qualidade | E13 | Meta de 70% de branches | RN-10 | MUST | Relatório JaCoCo |
| RNF-04 | RNF | Rastreabilidade de requisitos críticos | Transversal | Estratégia de qualidade | E13 | 100% rastreados | RN-10 | MUST | Matriz revisada |
| RNF-05 | RNF | Bugs críticos conhecidos | Transversal | Estratégia de qualidade | E13 | Zero bugs críticos | RN-10 | MUST | Relatório QA |
| RNF-06 | RNF | Vulnerabilidades críticas conhecidas | Transversal | Estratégia de qualidade | E13 | Zero vulnerabilidades críticas | RN-10 | MUST | SonarCloud e relatório de segurança |
| RNF-07 | RNF | Validação automatizada de persistência crítica | Solicitante; Responsável; Administrador | Estratégia de qualidade | E13 | Persistência realista | RN-09 | MUST | Testcontainers |
| RNF-08 | RNF | Validação de integrações externas | Transversal | Estratégia de qualidade | E9 | Integração verificada | RN-06; RN-09 | MUST | WireMock ou integração |
| RNF-09 | RNF | Testes de concorrência | Solicitante; Administrador | Estratégia e regras críticas | E13 | Uma reserva aceita | RN-04 | MUST | Teste concorrente |
| RNF-10 | RNF | Testes automatizados em camadas | Transversal | Estratégia de qualidade | E13 | Cinco tipos de teste | RN-10 | MUST | Relatórios de testes |
| RNF-11 | RNF | TDD ou BDD em funcionalidade nova | Transversal | Estratégia de qualidade | E13 | Pelo menos uma funcionalidade | RN-10 | MUST | Evidência TDD/BDD |
| RNF-12 | RNF | Integração contínua em pull requests | Transversal | Estratégia de qualidade | E13 | GitHub Actions em PRs | RN-10 | MUST | Workflow executado |
| RNF-13 | RNF | Análise estática | Transversal | Estratégia de qualidade | E13 | SonarCloud e zero vulnerabilidades críticas | RN-10 | MUST | Resultado SonarCloud |
| RNF-14 | RNF | Desempenho sob carga | Solicitante; Responsável; Administrador | Estratégia de qualidade | E13 | Valor pendente | RN-10 | MUST | Relatório JMeter |
| RNF-15 | RNF | Segurança de autenticação, autorização, entrada e erros | Solicitante; Responsável; Administrador | Requisitos 1 e 13 e estratégia | E1 | Testes positivos/negativos e zero exposição | RN-06 | MUST | Testes e relatório de segurança |
| RNF-16 | RNF | Responsividade e acessibilidade | Solicitante; Responsável; Administrador | Requisito 13 e RF-22 | E11 | Viewports pendentes | RN-10 | MUST | Relatório de interface |
| RNF-17 | RNF | Mensagens de erro compreensíveis | Solicitante; Responsável; Administrador | Requisito 13 e RF-22 | E11 | Erros críticos cobertos | RN-01; RN-02; RN-05 | MUST | Testes e revisão QA |
| RNF-18 | RNF | Documentação verificável dos fluxos públicos | Transversal | Requisito 14 e RF-23 | E12 | Itens públicos documentados | RN-10 | MUST | Documentação revisada |

## 10. Cobertura por Persona

| Persona | RFs relacionados | RNFs relacionados | Permissões cobertas | Restrições cobertas | Lacunas |
|---|---|---|---|---|---|
| Solicitante | RF-01, RF-08, RF-09, RF-10, RF-11, RF-12, RF-13, RF-18, RF-19, RF-22 | RNF-07, RNF-09, RNF-14, RNF-15, RNF-16, RNF-17 | Consulta e pesquisa; criação, alteração e cancelamento das próprias reservas | Sem reservas de terceiros; sem recursos em manutenção; sem dupla reserva; sem aprovação, validação ou gestão administrativa | Canal e momento de notificações pendentes de decisão |
| Responsável | RF-01, RF-14, RF-15, RF-16, RF-17, RF-18, RF-19, RF-22 | RNF-07, RNF-08, RNF-14, RNF-15, RNF-16, RNF-17 | Aprovação de solicitações especiais; validação de docentes; retirada e devolução | Sem gestão administrativa; sem reservas de terceiros; aprovação somente em sua responsabilidade | Limites operacionais da aprovação não especificados |
| Administrador | RF-01, RF-02, RF-03, RF-04, RF-05, RF-06, RF-07, RF-08, RF-09, RF-13, RF-19, RF-21, RF-22 | RNF-04, RNF-05, RNF-06, RNF-07, RNF-09, RNF-13, RNF-14, RNF-15, RNF-16, RNF-17 | Gestão de salas, professores, materiais, usuários, bloqueios, manutenção; relatórios e histórico | Sem permitir conflitos ou reservas em manutenção; sem apagar reservas iniciadas; sem substituir Responsável | Escopo exato de cada operação de gestão pendente de detalhamento da equipe |

## 11. Cobertura do Escopo

| Escopo | Descrição | RFs | RNFs | Cobertura | Lacunas |
|---|---|---|---|---|---|
| E1 | Acesso e Perfis | RF-01, RF-05 | RNF-06, RNF-15 | Coberto | Detalhes de sessão pendentes |
| E2 | Cadastro de Recursos | RF-02, RF-03, RF-04 | RNF-01 | Coberto | Campos de cadastro não especificados |
| E3 | Pesquisa e Disponibilidade | RF-08, RF-09 | RNF-14, RNF-15, RNF-16, RNF-17 | Coberto | Metas de desempenho pendentes |
| E4 | Reservas e Agenda | RF-10, RF-11, RF-12, RF-13, RF-18 | RNF-07, RNF-09, RNF-14 | Coberto | Transições não especificadas pendentes |
| E5 | Aprovação de Recursos Restritos | RF-14, RF-15 | RNF-15 | Coberto | Critérios de solicitação especial pendentes |
| E6 | Manutenção e Bloqueios | RF-06, RF-07 | RNF-15, RNF-17 | Coberto | Relação entre bloqueio e manutenção pendente |
| E7 | Retirada e Devolução de Materiais | RF-16, RF-17 | RNF-07 | Coberto | Estados detalhados de movimentação pendentes |
| E8 | Auditoria e Histórico | RF-19 | RNF-04, RNF-06, RNF-07, RNF-18 | Coberto | Retenção e formato do histórico pendentes |
| E9 | Notificações e Integrações | RF-20 | RNF-08 | Coberto | Escolha entre simulação e API externa pendente |
| E10 | Relatórios | RF-21 | RNF-14 | Coberto | Filtros e formato dos relatórios pendentes |
| E11 | Interface, Erros e Acessibilidade | RF-22 | RNF-15, RNF-16, RNF-17 | Coberto | Viewports e critérios de acessibilidade pendentes |
| E12 | Documentação da API ou Fluxos Públicos | RF-23 | RNF-18 | Coberto | Forma documental pendente |
| E13 | Qualidade, Segurança, Desempenho e CI | RF-01, RF-13, RF-19, RF-20, RF-22 | RNF-01 a RNF-17 | Coberto | Portões adicionais pendentes |

## 12. Cobertura dos Requisitos Oficiais

| Requisito oficial | RFs/RNFs relacionados | Coberto? | Observação |
|---|---|---|---|
| 1. Autenticação e autorização por perfil | RF-01, RF-05, RNF-15 | Sim | Três perfis oficiais cobertos com casos positivos e negativos. |
| 2. Cadastro e consulta de salas, professores e materiais | RF-02, RF-03, RF-04, RF-08, RF-15 | Sim | Cadastro, consulta e validação de docentes estão separados. |
| 3. Pesquisa por tipo, capacidade, localização, competência e disponibilidade | RF-09 | Sim | Filtros e disponibilidade estão no mesmo requisito atômico de pesquisa. |
| 4. Criação, alteração e cancelamento de reservas | RF-10, RF-11, RF-12, RF-18 | Sim | Operações e estados foram decompostos. |
| 5. Detecção de sobreposição, inclusive agenda do professor | RF-09, RF-13, RF-15 | Sim | Sala, material e professor estão explicitamente cobertos. |
| 6. Proteção contra dupla reserva simultânea | RF-13, RNF-09 | Sim | Há cenário e teste automatizado de concorrência. |
| 7. Aprovação obrigatória para recursos restritos | RF-14, RF-18, RNF-15 | Sim | Somente Responsável aprova. |
| 8. Bloqueio de recursos em manutenção | RF-06, RF-07, RF-09, RF-10, RF-11 | Sim | Manutenção e bloqueio afetam disponibilidade e reserva. |
| 9. Registro de retirada e devolução | RF-16, RF-17 | Sim | Responsável registra e acompanha as duas operações. |
| 10. Histórico auditável de mudanças | RF-19, RNF-04, RNF-06 | Sim | Mudanças de estado geram registros auditáveis. |
| 11. Notificação simulada ou integração com API externa | RF-20, RNF-08 | Sim | A alternativa concreta ainda requer decisão da equipe. |
| 12. Relatório de utilização, carga horária e conflitos evitados | RF-21 | Sim | Os três indicadores estão no resultado esperado. |
| 13. Interface responsiva e mensagens de erro compreensíveis | RF-22, RNF-16, RNF-17 | Sim | Critérios observáveis e métricas pendentes quando não oficiais. |
| 14. Documentação da API ou fluxos públicos | RF-23, RNF-18 | Sim | API ou fluxos públicos devem ser escolhidos e documentados. |

## 13. Candidatos para Avaliação da Equipe

Os itens abaixo foram identificados durante a análise, mas não possuem suporte suficiente para entrar na baseline como requisito aprovado.

### Candidato 1: Canal e conteúdo da notificação

- **Descrição:** definir canal, destinatário, conteúdo e evento exato da notificação.
- **Origem da ideia:** RF-20 e requisito oficial 11.
- **Benefício:** permitiria validar de forma mais específica a comunicação do fluxo.
- **Risco:** escolher canal, destinatário ou evento sem decisão oficial criaria escopo de negócio.
- **Decisão necessária:** escolher notificação simulada ou API externa e definir evento, canal e destinatário.
- **Status:** NÃO APROVADO.

### Candidato 2: Metas de tempo de resposta e carga

- **Descrição:** estabelecer tempos-alvo, volume de usuários, taxa de erro e duração do teste de carga.
- **Origem da ideia:** RNF-14 e uso de JMeter.
- **Benefício:** tornaria o desempenho passível de aprovação numérica.
- **Risco:** qualquer número seria uma decisão inventada sem aprovação.
- **Decisão necessária:** aprovar carga, percentis de resposta, taxa de erro e duração.
- **Status:** NÃO APROVADO.

### Candidato 3: Padrão de acessibilidade e viewports

- **Descrição:** definir padrão de acessibilidade, dispositivos e viewports oficiais de validação.
- **Origem da ideia:** RF-22 e RNF-16.
- **Benefício:** permitiria uma validação uniforme da interface.
- **Risco:** adotar padrão ou tamanhos não fornecidos alteraria o critério oficial.
- **Decisão necessária:** aprovar viewports, dispositivos e critérios de acessibilidade.
- **Status:** NÃO APROVADO.

### Candidato 4: Política de retenção do histórico auditável

- **Descrição:** definir por quanto tempo e com quais campos o histórico deve ser mantido.
- **Origem da ideia:** RF-19 e RN-09.
- **Benefício:** detalharia a operação de auditoria.
- **Risco:** prazo e campos não foram especificados.
- **Decisão necessária:** aprovar retenção e conteúdo mínimo do histórico.
- **Status:** NÃO APROVADO.

### Candidato 5: Transições e operações em estados não descritas

- **Descrição:** definir quais perfis podem executar cada transição entre estados alternativos e o que ocorre após `EM_USO`, `CONCLUIDA`, `REJEITADA`, `CANCELADA` e `NAO_COMPARECEU`.
- **Origem da ideia:** RF-18 e RN-07.
- **Benefício:** eliminaria ambiguidades de fluxo.
- **Risco:** inventar transições mudaria as regras oficiais.
- **Decisão necessária:** aprovar somente as transições adicionais necessárias.
- **Status:** NÃO APROVADO.

### Candidato 6: Campos e filtros detalhados de relatórios

- **Descrição:** definir filtros, período, formato e nível de agrupamento dos relatórios.
- **Origem da ideia:** RF-21.
- **Benefício:** permitiria especificar a consulta operacional.
- **Risco:** campos e formatos adicionais não estão no requisito oficial.
- **Decisão necessária:** aprovar filtros e formato dos relatórios.
- **Status:** NÃO APROVADO.

## 14. Pendências para Decisão da Equipe

- Aprovar metas de desempenho do JMeter: carga, tempo de resposta, taxa de erro, duração e unidade, pois não há valores oficiais.
- Aprovar viewports, dispositivos e critérios objetivos de acessibilidade e responsividade.
- Escolher entre notificação simulada e integração com API externa; definir evento, canal, destinatário e contrato, sem tratar a escolha como baseline antes da aprovação.
- Especificar transições não descritas entre os estados oficiais, especialmente para `REJEITADA`, `CANCELADA`, `NAO_COMPARECEU`, `EM_USO` e `CONCLUIDA`.
- Definir o que caracteriza uma solicitação especial e um recurso restrito, pois a fonte exige aprovação, mas não detalha seus critérios.
- Confirmar os limites operacionais do Responsável ao aprovar solicitações especiais e recursos restritos.
- Definir campos, filtros, período e formato dos relatórios.
- Definir campos, retenção e consulta do histórico auditável.
- Definir campos obrigatórios e regras de validação dos cadastros de salas, professores, materiais e usuários.
- Definir a relação operacional entre bloqueios e períodos de manutenção.
- Definir critérios e quantidade de cenários para os RNFs que exigem "todos os fluxos críticos" quando a fonte não fornece contagem.
- Definir critérios de aprovação adicionais para GitHub Actions em pull requests, além da exigência de execução.

## 15. Checklist de Validação Final

- [x] PASSOU: as três personas foram lidas integralmente.
- [x] PASSOU: somente as três personas oficiais foram utilizadas.
- [x] PASSOU: todos os requisitos foram classificados como RF ou RNF.
- [x] PASSOU: todos os RFs descrevem comportamento observável.
- [x] PASSOU: todos os RFs possuem critérios testáveis.
- [x] PASSOU: todos os RNFs possuem métrica e validação objetiva.
- [x] PASSOU: termos vagos foram removidos ou associados a critério mensurável e pendência.
- [x] PASSOU: todos os requisitos possuem numeração contínua sem lacunas dentro de RF e RNF.
- [x] PASSOU: todos os requisitos possuem persona ou origem transversal justificada.
- [x] PASSOU: todos os requisitos estão ligados a um escopo E1 a E13.
- [x] PASSOU: os 14 requisitos funcionais oficiais estão cobertos.
- [x] PASSOU: as regras críticas estão cobertas.
- [x] PASSOU: concorrência e dupla reserva estão cobertas.
- [x] PASSOU: autenticação e autorização por perfil estão cobertas.
- [x] PASSOU: manutenção e bloqueio estão cobertos.
- [x] PASSOU: auditoria de mudança de estado está coberta.
- [x] PASSOU: retirada e devolução estão cobertas.
- [x] PASSOU: notificações ou integração externa estão cobertas.
- [x] PASSOU: relatórios estão cobertos.
- [x] PASSOU: metas de cobertura e qualidade estão registradas.
- [x] PASSOU: não existem requisitos duplicados na baseline.
- [x] PASSOU: não existem funcionalidades do Foot Fanatics.
- [x] PASSOU: não existem decisões inventadas apresentadas como aprovadas.
- [x] PASSOU: a matriz de rastreabilidade está completa para todos os RFs e RNFs.
- [x] PASSOU: o conteúdo foi salvo em `docs/prd.md`.

### Revisão cruzada

- **Analyst:** PASSOU. Cada requisito está ligado a persona ou requisito oficial, regra aplicável e escopo oficial.
- **Product Manager:** PASSOU. Duplicidades foram consolidadas, o escopo foi limitado a E1-E13 e decisões pendentes não foram apresentadas como aprovadas.
- **QA:** PASSOU. RFs possuem critérios observáveis; RNFs possuem métrica, valor-alvo, condição e método; persistência crítica, concorrência, autorização e evidências foram cobertas.
- **Architect:** PASSOU. Permissões, manutenção, agenda do professor, concorrência, auditoria, reserva iniciada e estados oficiais estão coerentes; transições não especificadas foram mantidas como pendência.

## Resultado da Elicitação

- **Total de RFs:** 23.
- **Total de RNFs:** 18.
- **Total de regras de negócio:** 10.
- **Total de candidatos não aprovados:** 6.
- **Pendências para decisão humana:** 12 grupos de decisão, listados na seção 14.
- **Confirmação:** todos os requisitos estão numerados; RNFs possuem métrica, valor-alvo, unidade, condição, método e critério de aprovação; todos os requisitos estão ligados às personas ou à origem transversal justificada e a um escopo E1-E13; a rastreabilidade está registrada na matriz.
