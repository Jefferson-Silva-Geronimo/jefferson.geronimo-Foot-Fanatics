# Fluxos e Contexto das Personas

## 1. Controle do Documento

- **Finalidade:** documentar o contexto, as jornadas, as interações e os fluxos operacionais das personas do sistema Organização de Recursos.
- **Versão:** 1.0.
- **Data:** 2026-08-28.
- **Status:** Baseline para revisão da equipe.
- **Documentos utilizados:** `docs/personas/solicitante.md`, `docs/personas/responsavel.md`, `docs/personas/administrador.md`, `docs/prd.md` e `README.md`.
- **Documentos ausentes:** nenhum dos documentos obrigatórios estava ausente. O `README.md` contém apenas a identificação do projeto como atividade de aula e não acrescenta requisitos de domínio.
- **Responsáveis pela revisão:** Analyst, Product Manager, Architect e QA do AIOX Squad foram utilizados como papéis de revisão; a aprovação final permanece com a equipe do projeto.
- **Observação:** nenhuma execução de teste, integração, pipeline ou ferramenta de qualidade é declarada neste documento. As evidências descritas são esperadas ou sugeridas para validação futura.

## 2. Visão Geral do Sistema

### Problema

A alocação de salas, professores e materiais precisa ocorrer sem conflitos de horário, inclusive na agenda do professor, e deve preservar rastreabilidade, auditoria, segurança e controle operacional.

### Objetivo

Desenvolver e validar uma aplicação que organize a alocação de salas, professores e materiais sem conflitos de horário, apresentando evidências objetivas de qualidade, segurança, rastreabilidade e desempenho.

### Recursos gerenciados

- Salas.
- Professores, que podem ser recursos alocáveis.
- Materiais e equipamentos.
- Usuários e os três perfis oficiais.
- Bloqueios e períodos de manutenção.
- Reservas, estados, retiradas, devoluções, histórico, notificações e relatórios.

### Valor esperado

- Evitar sobreposição de reservas e dupla reserva simultânea.
- Impedir o uso de recursos em manutenção ou bloqueados.
- Controlar a aprovação de recursos restritos.
- Acompanhar a movimentação de materiais.
- Produzir histórico auditável e relatórios operacionais.

### Limites do sistema

O sistema utiliza exclusivamente os perfis Solicitante, Responsável e Administrador. O projeto Foot Fanatics é somente demonstrativo e não fornece entidades, perfis, escopos ou funcionalidades para este sistema.

## 3. Fontes e Premissas

### Requisitos oficiais

Os requisitos funcionais, regras críticas, estados, estratégias de qualidade e escopos E1 a E13 estão em `docs/prd.md` e no contexto oficial desta tarefa.

### Informações obtidas das personas

As personas definem os objetivos, responsabilidades, permissões, restrições, funcionalidades utilizadas e critérios de sucesso de cada perfil. Os arquivos foram analisados integralmente.

### Informação obtida do README

O README apenas identifica `jefferson.geronimo-Foot-Fanatics` como projeto em aula. Não há requisito adicional de Organização de Recursos nele.

### Premissas de leitura

- Professor como usuário é distinto de professor como recurso.
- Um professor pode atuar como usuário com perfil Solicitante, mas a relação entre conta e recurso professor não está formalizada.
- O fluxo principal oficial é `SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA`.
- Os estados alternativos oficiais são `REJEITADA`, `CANCELADA` e `NAO_COMPARECEU`.
- A pesquisa de disponibilidade não substitui a validação no momento da reserva.
- Toda transição de estado deve gerar auditoria.

### Pendências

Qualquer decisão não expressa pelas fontes é tratada como pendência, candidato não aprovado ou `PENDENTE DE DECISÃO DA EQUIPE`. Não são definidos mecanismos técnicos específicos para concorrência, autenticação, armazenamento, integração ou notificações.

## 4. Personas Oficiais

### 4.1 Solicitante

#### Identificação do perfil

- **Nome do perfil:** Solicitante.
- **Definição oficial:** Professor ou coordenador que consulta a disponibilidade e cria, altera ou cancela suas reservas.
- **Arquivo de origem:** `docs/personas/solicitante.md`.
- **Papel dentro do sistema:** iniciar e manter suas próprias solicitações de reserva.

#### Contexto de atuação

Participa quando precisa consultar recursos e organizar uma reserva. Resolve a necessidade de encontrar sala, professor, material ou equipamento disponível sem conflito. Visualiza cadastro, filtros, disponibilidade, período, estado e mensagens observáveis das próprias operações. Interage com salas, professores, materiais, equipamentos e com a agenda do professor como recurso. O Responsável participa quando há recurso restrito ou necessidade de validação/aprovação; o Administrador prepara cadastros, bloqueios e manutenção.

#### Objetivo principal

Organizar suas reservas de salas, professores e materiais sem conflitos de horário.

#### Objetivos secundários

- Encontrar recursos compatíveis com a necessidade da reserva.
- Confirmar a disponibilidade no período desejado.
- Criar, alterar ou cancelar suas próprias reservas.
- Evitar conflitos na sala, no material e na agenda do professor.

#### Responsabilidades

- Consultar a disponibilidade de recursos.
- Criar suas reservas.
- Alterar suas reservas.
- Cancelar suas reservas.

#### Necessidades de informação

- Tipo, capacidade, localização e competência do recurso.
- Disponibilidade no período desejado.
- Situação de reserva, bloqueio e manutenção.
- Agenda do professor alocado.
- Estado e resultado das próprias solicitações.
- Motivo observável de conflito, indisponibilidade, período inválido ou acesso negado.
- Histórico auditável que estiver disponível conforme a autorização definida.

#### Funcionalidades utilizadas

- Autenticação e autorização.
- Consulta de recursos.
- Pesquisa de disponibilidade.
- Criação, alteração e cancelamento de reservas.
- Recebimento de notificações relacionadas, quando a alternativa de notificação for definida.

#### Permissões

- Consultar recursos e pesquisar sua disponibilidade.
- Criar reservas.
- Alterar suas próprias reservas quando permitido pelas regras.
- Cancelar suas próprias reservas quando permitido pelas regras.
- Acompanhar o resultado e o estado das próprias solicitações, conforme a visibilidade definida pela equipe.

#### Restrições

- Não pode criar, alterar ou cancelar reservas de outros Solicitantes.
- Não pode reservar recursos em manutenção ou bloqueados.
- Não pode gerar dupla reserva.
- Não pode aprovar recursos restritos ou sua própria solicitação.
- Não pode validar a alocação de docentes.
- Não pode gerenciar salas, professores, materiais, usuários, bloqueios ou manutenção.
- Não pode apagar reserva iniciada.

#### Decisões realizadas

- Seleciona recursos, filtros e período para sua solicitação.
- Decide criar, alterar ou cancelar sua própria reserva quando a operação estiver permitida.
- Não decide aprovação de recurso restrito, validação docente, transições não especificadas ou gestão administrativa.

#### Eventos que iniciam sua atuação

- Necessidade de reservar uma sala, professor, material ou equipamento.
- Necessidade de consultar disponibilidade.
- Necessidade de alterar ou cancelar uma reserva própria ainda não iniciada, quando permitido.

#### Resultados esperados

A solicitação é criada sem conflito ou a alteração/cancelamento é efetivado conforme as regras. O sistema informa o estado, impede operações proibidas e mantém as mudanças rastreáveis.

#### Erros e impedimentos possíveis

- Acesso negado.
- Dados ou período inválidos.
- Término igual ou anterior ao início.
- Conflito na sala, material, equipamento ou agenda do professor.
- Recurso inexistente, indisponível, bloqueado ou em manutenção.
- Solicitação concorrente vencida por outra reserva.
- Reserva de outro Solicitante.
- Tentativa de alteração ou cancelamento de reserva iniciada.
- Falha na notificação ou integração externa.

#### Auditoria relacionada

Mudanças de estado de suas reservas devem gerar auditoria. Criação, alteração, cancelamento e demais operações auditáveis devem seguir a definição da equipe; não se presume um formato ou retenção.

#### Notificações relacionadas

Pode receber informação sobre o resultado da solicitação, aprovação, rejeição, cancelamento ou falha de comunicação quando esses eventos e o canal forem definidos. Evento, canal, destinatário e conteúdo permanecem pendentes.

#### Critérios de sucesso

- Consulta os recursos e a disponibilidade corretos para o período.
- Cria reserva sem sobreposição e sem recurso indisponível.
- Altera ou cancela somente suas próprias reservas permitidas.
- Recebe motivo observável quando a operação é recusada.
- As mudanças de estado ficam auditáveis.

#### Riscos relacionados

- Autorização incorreta permitindo acesso à reserva de outro usuário.
- Dupla reserva ou sobreposição da agenda do professor.
- Reserva de recurso em manutenção ou bloqueado.
- Alteração sem auditoria.
- Informação de erro insuficiente ou insegura.
- Dados de disponibilidade desatualizados entre pesquisa e confirmação.

#### Jornada resumida

Autentica-se, consulta e filtra recursos, verifica disponibilidade de sala, material e professor, cria a solicitação com horário válido, acompanha aprovação quando necessária, utiliza o recurso quando o fluxo permitir e altera ou cancela sua reserva dentro das regras. As mudanças são registradas para rastreabilidade.

### 4.2 Responsável

#### Identificação do perfil

- **Nome do perfil:** Responsável.
- **Definição oficial:** Aprova solicitações especiais, valida a alocação de docentes e acompanha retiradas e devoluções de material.
- **Arquivo de origem:** `docs/personas/responsavel.md`.
- **Papel dentro do sistema:** decidir sobre solicitações especiais sob sua responsabilidade, validar docentes e acompanhar movimentações de material.

#### Contexto de atuação

Participa quando existe solicitação especial de recurso restrito, alocação docente a validar ou movimentação de material. Precisa visualizar a solicitação, o recurso, o período, a disponibilidade, a agenda do professor, a reserva e os registros de retirada/devolução. Decide aprovação ou rejeição conforme as regras aplicáveis e valida a alocação docente. Interage com o Solicitante por meio da solicitação e com o Administrador por meio dos recursos e configurações, sem assumir a gestão administrativa.

#### Objetivo principal

Garantir a aprovação de solicitações especiais, a validação da alocação de docentes e o acompanhamento dos materiais retirados e devolvidos.

#### Objetivos secundários

- Avaliar solicitações de recursos restritos.
- Confirmar que a alocação docente não conflita com a agenda do professor.
- Registrar e acompanhar retirada e devolução de materiais e equipamentos.
- Preservar a rastreabilidade das decisões e movimentações.

#### Responsabilidades

- Aprovar solicitações especiais.
- Validar a alocação de docentes.
- Acompanhar retiradas de material.
- Acompanhar devoluções de material.

#### Necessidades de informação

- Solicitação especial pendente e recurso restrito relacionado.
- Solicitante e informações disponíveis para a decisão.
- Período solicitado e disponibilidade atual.
- Agenda do professor e conflitos existentes.
- Reserva e material/equipamento associado.
- Retirada registrada e devolução correspondente.
- Estado atual e histórico auditável das operações.

#### Funcionalidades utilizadas

- Autenticação e autorização.
- Aprovação de solicitações especiais.
- Validação de docentes.
- Registro de retirada de materiais.
- Registro de devolução de materiais.
- Acompanhamento de estados, histórico e notificações quando autorizados e definidos.

#### Permissões

- Aprovar ou rejeitar solicitações especiais sob sua responsabilidade, conforme regras definidas.
- Validar a alocação de docentes.
- Acompanhar e registrar retiradas de materiais e equipamentos.
- Acompanhar e registrar devoluções correspondentes.
- Consultar informações necessárias aos fluxos em que participa, conforme autorização definida.

#### Restrições

- Não pode gerenciar salas, professores, materiais, usuários, bloqueios ou manutenção.
- Não pode criar, alterar ou cancelar reservas de outros Solicitantes.
- Não pode aprovar recursos restritos fora de sua responsabilidade.
- Não pode aprovar quando existir conflito ou quando a disponibilidade não tiver sido validada novamente.
- Não pode substituir o Administrador na gestão de cadastros.
- Não pode alterar registros de auditoria.

#### Decisões realizadas

- Decide aprovar ou rejeitar solicitação especial quando autorizado.
- Decide o resultado da validação da alocação docente conforme a agenda do professor.
- Registra retirada e devolução de material quando as pré-condições forem atendidas.
- Não decide transições de estado não especificadas, critérios de recurso restrito, políticas de manutenção ou permissões administrativas.

#### Eventos que iniciam sua atuação

- Recebimento ou existência de solicitação especial pendente.
- Necessidade de validar alocação de docente.
- Existência de material ou equipamento associado a uma reserva para retirada.
- Existência de retirada registrada para devolução.

#### Resultados esperados

A solicitação é aprovada ou rejeitada de forma autorizada, a alocação docente é validada sem conflito e as retiradas e devoluções ficam registradas e acompanháveis. As decisões e mudanças aplicáveis geram auditoria.

#### Erros e impedimentos possíveis

- Acesso negado.
- Solicitação inexistente, já decidida ou fora de sua responsabilidade.
- Conflito na agenda do professor.
- Disponibilidade alterada antes da decisão.
- Recurso em manutenção ou bloqueado.
- Tentativa de aprovação por perfil indevido.
- Devolução sem retirada correspondente.
- Retirada ou devolução duplicada, se a regra for confirmada.
- Transição não permitida.
- Falha na notificação ou integração externa.

#### Auditoria relacionada

Aprovação, rejeição, validação docente e mudanças de estado devem ser auditadas. Retirada, devolução e tentativas recusadas devem seguir a política de auditoria definida pela equipe; a exigência de auditoria de mudança de estado é oficial.

#### Notificações relacionadas

Pode receber solicitações e resultados de decisões ou movimentações. Solicitante e demais destinatários, eventos, canal e conteúdo não estão definidos e permanecem pendentes.

#### Critérios de sucesso

- Somente o Responsável autorizado decide sobre recurso restrito.
- A decisão considera a disponibilidade atual e não aceita conflito.
- A alocação docente sem sobreposição é registrada como validada.
- Retirada e devolução correspondentes ficam registradas.
- Estados e decisões relevantes ficam auditáveis.

#### Riscos relacionados

- Aprovação por perfil indevido ou fora da responsabilidade.
- Aprovação com disponibilidade desatualizada.
- Conflito ignorado na agenda do professor.
- Retirada sem registro ou devolução sem retirada.
- Alteração de estado sem auditoria.
- Notificação de decisão não produzida ou duplicada.

#### Jornada resumida

Autentica-se, consulta solicitações especiais e alocações, verifica recurso, período, disponibilidade e agenda docente, aprova ou rejeita quando autorizado, valida a alocação, acompanha a retirada, registra ou acompanha a devolução e consulta a rastreabilidade das decisões e movimentações.

### 4.3 Administrador

#### Identificação do perfil

- **Nome do perfil:** Administrador.
- **Definição oficial:** Gerencia salas, professores, materiais, usuários, bloqueios e períodos de manutenção.
- **Arquivo de origem:** `docs/personas/administrador.md`.
- **Papel dentro do sistema:** preparar e manter os cadastros, acessos, bloqueios e períodos de manutenção que sustentam a operação.

#### Contexto de atuação

Participa antes e durante a operação para manter recursos e acessos organizados. Resolve problemas de cadastro, indisponibilidade, bloqueio, manutenção e controle operacional. Visualiza salas, professores, materiais, usuários, perfis, bloqueios, manutenção, utilização, carga horária, conflitos evitados e histórico. Interage com o Solicitante ao sustentar a pesquisa e disponibilidade e com o Responsável sem substituir sua aprovação.

#### Objetivo principal

Manter recursos, usuários, bloqueios e períodos de manutenção organizados para permitir uma alocação sem conflitos de horário.

#### Objetivos secundários

- Manter salas, professores, materiais e equipamentos disponíveis para consulta e alocação.
- Gerenciar usuários e os três perfis oficiais.
- Registrar bloqueios e períodos de manutenção.
- Consultar utilização por recurso, carga horária, conflitos evitados e histórico.
- Preservar rastreabilidade e controle operacional.

#### Responsabilidades

- Gerenciar salas.
- Gerenciar professores.
- Gerenciar materiais.
- Gerenciar usuários.
- Gerenciar bloqueios.
- Gerenciar períodos de manutenção.

#### Necessidades de informação

- Dados cadastrais de salas, professores, materiais e equipamentos.
- Usuários e perfis oficiais.
- Períodos e situação de bloqueios e manutenção.
- Reservas afetadas por indisponibilidade.
- Utilização, carga horária e conflitos evitados.
- Histórico de mudanças e operações auditáveis.

#### Funcionalidades utilizadas

- Autenticação e autorização.
- Gestão de salas, professores e materiais.
- Gestão de usuários.
- Gestão de bloqueios.
- Gestão de manutenção.
- Relatórios.
- Histórico auditável.

#### Permissões

- Gerenciar salas, professores, materiais, usuários, bloqueios e períodos de manutenção.
- Consultar relatórios operacionais.
- Consultar o histórico auditável conforme a autorização definida.
- Manter os perfis oficiais Solicitante, Responsável e Administrador, sem criar perfis adicionais.

#### Restrições

- Não pode permitir alocação com conflito de horário.
- Não pode permitir reserva de recurso em manutenção ou bloqueado.
- Não pode apagar reservas iniciadas nem apagar registros necessários ao histórico.
- Não pode substituir a aprovação do Responsável para recursos restritos.
- Não pode usar privilégios administrativos para contornar regras críticas.
- Não pode criar perfis fora dos três oficiais.
- Não pode alterar registros de auditoria.

#### Decisões realizadas

- Decide cadastrar e manter recursos, usuários, bloqueios e períodos de manutenção dentro do escopo.
- Decide quais dados administrativos precisam ser atualizados conforme as operações permitidas.
- Não decide aprovação de recurso restrito, transições não especificadas, fórmula de conflitos evitados ou políticas ainda pendentes.

#### Eventos que iniciam sua atuação

- Necessidade de cadastrar ou atualizar sala, professor, material ou equipamento.
- Necessidade de gerenciar usuário ou perfil oficial.
- Necessidade de bloquear recurso ou registrar manutenção.
- Necessidade de consultar relatórios ou histórico operacional.

#### Resultados esperados

Cadastros, perfis, bloqueios e manutenções ficam registrados e são considerados pela pesquisa e disponibilidade. Relatórios e histórico apoiam controle operacional, sem permitir conflito, reserva indevida ou perda de rastreabilidade.

#### Erros e impedimentos possíveis

- Acesso negado.
- Dados cadastrais inválidos ou recurso inexistente.
- Tentativa de criar perfil não oficial.
- Bloqueio ou manutenção com dados incompletos.
- Impacto em reserva existente sem política definida.
- Tentativa de permitir reserva em período indisponível.
- Tentativa de apagar reserva iniciada ou histórico.
- Tentativa de aprovar recurso restrito.
- Relatório sem dados ou com critérios ainda indefinidos.
- Falha na integração de notificação.

#### Auditoria relacionada

Alterações de recursos, usuários, perfis, bloqueios, manutenção, reservas e estados devem ser rastreáveis conforme a política aprovada. Toda mudança de estado de reserva deve gerar auditoria; retenção, campos e visibilidade do histórico permanecem pendentes.

#### Notificações relacionadas

Pode ser informado sobre falhas ou efeitos operacionais quando o mecanismo for definido. Não se presume canal, conteúdo, destinatário, prazo ou evento.

#### Critérios de sucesso

- Cadastros e perfis oficiais estão disponíveis para as operações autorizadas.
- Bloqueios e manutenção afetam pesquisa e disponibilidade.
- Não são permitidos conflitos ou reservas em indisponibilidade.
- Relatórios apresentam utilização, carga horária e conflitos evitados conforme definição aprovada.
- Histórico sustenta rastreabilidade e auditoria.

#### Riscos relacionados

- Gestão de acesso incorreta.
- Manutenção ou bloqueio ignorado pela pesquisa/reserva.
- Alteração administrativa sem auditoria.
- Exclusão de reserva iniciada ou de histórico.
- Contorno indevido da aprovação do Responsável.
- Relatório inconsistente.
- Dados cadastrais desatualizados.

#### Jornada resumida

Autentica-se, gerencia recursos e usuários, registra bloqueios e manutenção, verifica impacto na disponibilidade, consulta relatórios e histórico e mantém as regras de conflito, indisponibilidade, auditoria e aprovação exclusiva do Responsável.

## 5. Interação entre as Personas

### Dependências

1. O Administrador cadastra recursos e usuários e mantém bloqueios e manutenção.
2. O Solicitante consulta esses dados e cria, altera ou cancela suas próprias reservas.
3. O Responsável participa quando existe solicitação especial ou validação docente e acompanha materiais.
4. O sistema verifica sala, material, equipamento e professor em todas as operações de reserva.
5. A auditoria registra mudanças de estado e os demais eventos conforme política definida.

### Troca de responsabilidade

- O Administrador prepara o contexto operacional, mas não substitui a aprovação do Responsável.
- O Solicitante inicia e mantém a própria reserva, mas não aprova recurso restrito.
- O Responsável decide sobre solicitações especiais e valida docentes, mas não administra cadastros.
- A relação direta de comunicação entre perfis, canal e prazo não está definida.

### Pontos de decisão

- Solicitante: seleção, período, criação, alteração ou cancelamento próprios quando permitidos.
- Responsável: aprovação/rejeição e validação docente quando autorizado.
- Administrador: gestão de recursos, usuários, bloqueios e manutenção.
- Equipe: estados, transições, critérios de restrição, notificações, relatórios e lacunas listadas na seção 16.

### Limites de autorização

- Somente Responsável aprova recursos restritos.
- Solicitante opera somente suas próprias reservas e não aprova a própria solicitação.
- Responsável não executa gestão administrativa.
- Administrador não contorna aprovação, conflitos, manutenção ou histórico.
- A proteção deve ocorrer no back-end, com resposta segura para acesso negado.

### Professor como usuário e como recurso

- **Professor como usuário:** pode ser o usuário que atua como Solicitante, pois a definição oficial do Solicitante inclui professor ou coordenador.
- **Professor como recurso:** é o docente selecionável na reserva, cuja agenda participa da detecção de sobreposição.
- A fonte não define se as duas representações são sempre a mesma pessoa, se possuem relação cadastral, se o professor-recurso precisa de conta, se pode reservar a si próprio ou quais dados pessoais são visíveis.
- Portanto, a autorização usa o perfil do usuário autenticado, enquanto a disponibilidade usa a agenda do professor-recurso; a relação entre ambos é pendência da equipe.

## 6. Ciclo de Vida da Reserva

### Estados oficiais

| Estado | Significado | Efeito sobre disponibilidade | Operações permitidas | Operações proibidas | Lacunas |
|---|---|---|---|---|---|
| `SOLICITADA` | Solicitação registrada aguardando o fluxo aplicável. | PENDENTE DE DECISÃO sobre se já ocupa o recurso. | Consulta e decisões oficialmente definidas. | Aprovação por Solicitante ou Administrador; transições não definidas. | Estado inicial de reserva não restrita e ocupação do recurso. |
| `APROVADA` | Solicitação aprovada. | Deve ser considerada no controle de conflito conforme regra aprovada. | Fluxo posterior oficialmente definido somente como `EM_USO`. | Operações não definidas e apagar reserva iniciada. | Cancelamento, alteração e ocupação exata. |
| `EM_USO` | Reserva iniciada. | Recursos estão em uso e não podem ser tratados como livres. | Operações necessárias ao uso e conclusão, conforme decisão. | Apagar reserva; alterações/transições não definidas. | Quem inicia e quando; retirada relacionada. |
| `CONCLUIDA` | Reserva concluída. | Liberação do recurso é PENDENTE DE DECISÃO. | Consulta e histórico conforme autorização. | Reabertura ou nova transição não definida. | Quem conclui e relação com devolução. |
| `REJEITADA` | Solicitação especial rejeitada. | Deve deixar de prosseguir como solicitação aprovada; efeito detalhado é pendente. | Consulta e histórico. | Reabertura ou alteração não definida. | Motivo obrigatório e transições seguintes. |
| `CANCELADA` | Reserva cancelada. | Liberação do recurso é PENDENTE DE DECISÃO. | Consulta e histórico. | Reabertura ou alteração não definida. | Estados de origem, motivo e liberação. |
| `NAO_COMPARECEU` | Reserva marcada por não comparecimento. | Efeito sobre disponibilidade é PENDENTE DE DECISÃO. | Consulta e histórico. | Reabertura ou transição não definida. | Origem, momento e perfil que registra. |

### Transições confirmadas ou explicitamente nomeadas

- `SOLICITADA -> APROVADA -> EM_USO -> CONCLUIDA`: fluxo principal oficial, sem definição completa dos atores e momentos.
- `SOLICITADA -> REJEITADA`: estado alternativo exigido para rejeição, com detalhes pendentes.
- `SOLICITADA -> CANCELADA`: possibilidade decorrente do cancelamento, mas condição e origem precisam de decisão.
- Qualquer outra transição: `PENDENTE DE DECISÃO DA EQUIPE`.

### Auditoria do ciclo

Toda mudança de estado deve gerar registro de auditoria. O cancelamento não significa exclusão física do histórico. A equipe ainda precisa definir campos, retenção, visibilidade, tentativas recusadas e imutabilidade operacional dos registros.

## 7. Fluxos Detalhados

### FLX-01: Autenticação e autorização

#### Objetivo

Permitir que um usuário autenticado acesse somente as operações do perfil oficial correspondente.

#### Personas participantes

- **Persona principal:** usuário de Solicitante, Responsável ou Administrador.
- **Personas de apoio:** Administrador gerencia usuários e perfis oficiais.
- **Sem permissão:** qualquer perfil tentando operação atribuída a outro perfil.

#### Gatilho

O usuário tenta entrar ou acessar uma operação do sistema.

#### Pré-condições

Usuário e perfil oficial existem; credenciais são recebidas pelo sistema.

#### Dados necessários

Credenciais, perfil autenticado e operação solicitada. Campos de autenticação não especificados permanecem pendentes.

#### Fluxo principal

1. O usuário envia suas credenciais; o sistema autentica e identifica o perfil; valida as credenciais; aplica autorização; registra auditoria somente se a política exigir; não há mudança de reserva; notificação não é definida.
2. O usuário solicita uma operação compatível; o sistema permite; valida o perfil; aplica RN de autorização; mantém os dados; gera evidência de acesso permitido.

#### Fluxos alternativos

- O Administrador gerencia a associação de um usuário a um dos três perfis oficiais.
- O usuário acessa outra operação compatível com seu mesmo perfil.

#### Fluxos de exceção

Credencial inválida, perfil não oficial, rota sem permissão ou tentativa de contornar autorização no back-end devem resultar em recusa e mensagem segura, sem stack trace, credenciais ou detalhes internos.

#### Pós-condições

A operação autorizada fica disponível; operação não autorizada não altera dados.

#### Regras de negócio relacionadas

RN-06 e RN-10 do PRD.

#### Requisitos relacionados

RF-01, RF-05, RF-22, RNF-06, RNF-15.

#### Auditoria esperada

Registro de operação efetivada conforme política de auditoria; falha de autorização e campos do registro permanecem pendentes.

#### Notificações esperadas

Nenhuma notificação específica foi definida.

#### Evidências e testes sugeridos

JUnit 5 para autorização isolada; testes parametrizados dos três perfis; API black-box positiva e negativa; E2E; SonarCloud e revisão de segurança.

#### Critérios de sucesso

Cada perfil acessa operações permitidas, operações indevidas são recusadas no back-end e erros não expõem detalhes internos.

#### Pendências

Sessão, expiração, múltiplos perfis, desativação de usuário e visibilidade de histórico.

### FLX-02: Cadastro e manutenção de recursos

#### Objetivo

Manter salas, professores, materiais e equipamentos disponíveis para consulta e alocação.

#### Personas participantes

- **Persona principal:** Administrador.
- **Personas de apoio:** Solicitante consulta; Responsável consulta informações necessárias.
- **Sem permissão:** Solicitante e Responsável não gerenciam cadastros.

#### Gatilho

Necessidade de cadastrar ou atualizar sala, professor, material ou equipamento.

#### Pré-condições

Administrador autenticado e tipo de recurso dentro do escopo.

#### Dados necessários

Tipo do recurso e dados cadastrais necessários; campos obrigatórios ainda não foram definidos.

#### Fluxo principal

1. Administrador seleciona o tipo e informa os dados; sistema valida entrada e autorização; aplica escopo E2; mantém o recurso; auditoria de alteração é pendente quando não houver mudança de estado.
2. Sistema disponibiliza o recurso para consulta e pesquisa; valida consistência e disponibilidade; aplica RN-02, RN-03 e RN-05 quando relevante; resultado é recurso consultável.

#### Fluxos alternativos

Cadastro ou consulta específica de sala, professor, material ou equipamento.

#### Fluxos de exceção

Dados inválidos, recurso inexistente, tipo fora do escopo, acesso indevido ou alteração que impacte reserva existente sem política definida devem ser recusados ou encaminhados à pendência correspondente.

#### Pós-condições

O cadastro atualizado pode influenciar pesquisa e disponibilidade conforme o estado registrado.

#### Regras de negócio relacionadas

RN-02, RN-03, RN-05 e RN-09.

#### Requisitos relacionados

RF-02, RF-03, RF-04, RF-08, RNF-07, RNF-15.

#### Auditoria esperada

Alteração cadastral rastreável conforme política aprovada; campos e retenção pendentes.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

JUnit 5 e parametrizados para validação; integração com Testcontainers; API black-box de cadastro, consulta e autorização; E2E de pesquisa após manutenção.

#### Critérios de sucesso

Recursos válidos são cadastrados e consultáveis; dados inválidos e gestão por perfil indevido não alteram o sistema.

#### Pendências

Campos, atualização, desativação, exclusão, relação professor-usuário e impacto sobre reservas existentes.

### FLX-03: Gestão de usuários e perfis

#### Objetivo

Manter usuários associados somente aos perfis oficiais de acesso.

#### Personas participantes

- **Persona principal:** Administrador.
- **Personas de apoio:** Solicitante e Responsável utilizam o perfil recebido.
- **Sem permissão:** Solicitante e Responsável não gerenciam usuários.

#### Gatilho

Necessidade de criar ou atualizar usuário ou perfil oficial.

#### Pré-condições

Administrador autenticado.

#### Dados necessários

Usuário e um dos perfis `Solicitante`, `Responsável` ou `Administrador`. Outros campos não foram especificados.

#### Fluxo principal

1. Administrador informa usuário e perfil oficial; sistema valida autorização e dados; aplica RN-06; salva a associação; auditoria conforme política; sem mudança de reserva.
2. Usuário autentica-se posteriormente; sistema identifica o perfil e aplica suas permissões; valida autorização; resultado é acesso restrito ao perfil.

#### Fluxos alternativos

Atualização de associação para qualquer um dos três perfis oficiais.

#### Fluxos de exceção

Perfil adicional, usuário inexistente, dado inválido, acesso de outro perfil ou impacto em reserva existente sem política aprovada devem ser recusados ou permanecer pendentes.

#### Pós-condições

Perfil oficial fica disponível para autorização.

#### Regras de negócio relacionadas

RN-06 e RN-10.

#### Requisitos relacionados

RF-01, RF-05, RNF-06, RNF-15.

#### Auditoria esperada

Alteração de perfil rastreável conforme política definida.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

API black-box, testes positivos/negativos dos três perfis, integração com persistência realista, E2E e SonarCloud.

#### Critérios de sucesso

Somente Administrador gerencia usuários; somente perfis oficiais são associados; acesso indevido não altera dados.

#### Pendências

Criação versus atualização, desativação, múltiplos perfis e efeito sobre reservas existentes.

### FLX-04: Pesquisa e consulta de disponibilidade

#### Objetivo

Encontrar recursos compatíveis e informar sua disponibilidade no período solicitado.

#### Personas participantes

- **Persona principal:** Solicitante.
- **Personas de apoio:** Administrador mantém os dados; Responsável consulta quando participa de decisão.
- **Sem permissão:** perfis sem autorização de consulta conforme definição da equipe.

#### Gatilho

Solicitante precisa encontrar sala, professor, material ou equipamento.

#### Pré-condições

Usuário autorizado; recursos cadastrados; período informado para pesquisa de disponibilidade.

#### Dados necessários

Tipo, capacidade, localização, competência, período e disponibilidade.

#### Fluxo principal

1. Solicitante informa filtros; sistema valida entrada; aplica autorização; consulta cadastro; mantém dados; sem mudança de estado.
2. Sistema verifica reservas, agenda do professor, bloqueios e manutenção; aplica RN-02, RN-03 e RN-05; retorna recursos compatíveis e reserváveis.

#### Fluxos alternativos

Consulta sem todos os filtros; consulta de cadastro sem período; resultado sem recursos compatíveis.

#### Fluxos de exceção

Filtro inválido, período inválido, recurso inexistente, indisponibilidade, manutenção, bloqueio ou acesso negado produzem resposta controlada e mensagem compreensível.

#### Pós-condições

O Solicitante possui resultado observável; nenhuma reserva é criada pela consulta.

#### Regras de negócio relacionadas

RN-01, RN-02, RN-03 e RN-05.

#### Requisitos relacionados

RF-08, RF-09, RF-13, RF-22, RNF-14, RNF-16, RNF-17.

#### Auditoria esperada

Consulta e tentativa recusada somente serão auditadas se a política aprovada exigir.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Testes parametrizados de filtros, API black-box, integração com Testcontainers e E2E com reservas, bloqueios, manutenção e agenda docente.

#### Critérios de sucesso

Cada filtro funciona conforme o escopo; recursos ocupados, bloqueados, em manutenção ou com conflito docente não aparecem como disponíveis.

#### Pendências

Campos de filtros, comportamento de intervalo adjacente e visibilidade exata para Responsável e Administrador.

### FLX-05: Criação de reserva

#### Objetivo

Registrar uma solicitação de reserva sem conflito e encaminhar recurso restrito à aprovação aplicável.

#### Personas participantes

- **Persona principal:** Solicitante.
- **Personas de apoio:** Responsável aprova recurso restrito; Administrador fornece cadastros e indisponibilidades.
- **Sem permissão:** Responsável e Administrador não criam reserva em nome de outro Solicitante.

#### Gatilho

Solicitante confirma sala, professor, material ou equipamento e período.

#### Pré-condições

Autenticação e autorização; recursos cadastrados; término posterior ao início; recurso livre e fora de manutenção/bloqueio.

#### Dados necessários

Recursos, tipo, período de início e término e indicação de recurso restrito quando definida.

#### Fluxo principal

1. Solicitante envia a solicitação; sistema valida autorização, datas e dados; aplica RN-01; prepara estado inicial, que é pendente para reserva não restrita.
2. Sistema verifica sobreposição em sala, material, equipamento e professor; aplica RN-02 e RN-03; rejeita conflito.
3. Sistema verifica concorrência no momento da confirmação; aplica RN-04; aceita no máximo uma solicitação simultânea.
4. Se recurso restrito exigir aprovação, sistema mantém `SOLICITADA` e encaminha ao Responsável; aplica RN-06.
5. Sistema gera auditoria da mudança efetivada; notificação depende da alternativa escolhida.

#### Fluxos alternativos

- Reserva não restrita: estado inicial e ocupação são `PENDENTE DE DECISÃO DA EQUIPE`.
- Recurso restrito: segue para decisão do Responsável.

#### Fluxos de exceção

Período inválido, conflito, manutenção, bloqueio, recurso inexistente, dupla reserva, acesso negado ou integração de notificação indisponível devem impedir inconsistência e apresentar mensagem controlada.

#### Pós-condições

Solicitação aceita conforme estado oficial aplicável ou recusada sem reserva inconsistente.

#### Regras de negócio relacionadas

RN-01, RN-02, RN-03, RN-04, RN-05, RN-06 e RN-07.

#### Requisitos relacionados

RF-10, RF-13, RF-18, RF-20, RNF-07, RNF-09, RNF-15.

#### Auditoria esperada

Registro da criação e da mudança de estado efetivada; conteúdo mínimo pendente.

#### Notificações esperadas

Resultado da solicitação e eventual aprovação/rejeição; evento, canal e destinatários pendentes.

#### Evidências e testes sugeridos

JUnit 5, testes parametrizados de horários, integração com Testcontainers, API, E2E, concorrência automatizada e WireMock para integração.

#### Critérios de sucesso

Término posterior ao início, nenhum recurso sobreposto, somente uma solicitação simultânea aceita, manutenção/bloqueio respeitados e recurso restrito submetido ao Responsável.

#### Pendências

Estado inicial não restrito, ocupação de `SOLICITADA`, definição de recurso restrito e critério de aprovação.

### FLX-06: Proteção contra dupla reserva

#### Objetivo

Impedir que solicitações simultâneas para o mesmo recurso e período produzam mais de uma reserva aceita.

#### Personas participantes

- **Persona principal:** Solicitantes concorrentes.
- **Personas de apoio:** Administrador consulta evidência; sistema executa validação.
- **Sem permissão:** operação concorrente não pode contornar autorização.

#### Gatilho

Duas solicitações chegam simultaneamente para o mesmo recurso e período.

#### Pré-condições

Recursos e período válidos; ambas as solicitações autorizadas.

#### Dados necessários

Mesmo recurso, mesmo período, duas solicitações e resultado de cada tentativa.

#### Fluxo principal

1. Sistema recebe as duas solicitações; valida datas e autorização; aplica RN-01.
2. Sistema verifica simultaneamente a disponibilidade do recurso; aplica RN-02, RN-03 e RN-04; preserva consistência.
3. Uma solicitação é aceita; sistema registra resultado e auditoria aplicável.
4. A outra é recusada de forma controlada; sistema não cria segunda reserva e apresenta conflito.

#### Fluxos alternativos

O mesmo cenário pode envolver sala, material, equipamento ou professor; a regra da agenda docente permanece aplicável.

#### Fluxos de exceção

Falha de persistência, resposta duplicada, inconsistência transacional, intervalo inválido ou acesso negado devem resultar em recusa controlada e sem dados parciais.

#### Pós-condições

Há no máximo uma reserva aceita para o mesmo recurso e período.

#### Regras de negócio relacionadas

RN-01, RN-02, RN-03 e RN-04.

#### Requisitos relacionados

RF-10, RF-13, RNF-07, RNF-09, RNF-14.

#### Auditoria esperada

Reserva aceita e resultado da tentativa recusada devem ser rastreáveis conforme política; RN-09 exige auditoria da mudança de estado efetivada.

#### Notificações esperadas

Resultado de cada tentativa, se o evento de notificação for definido.

#### Evidências e testes sugeridos

Teste automatizado de concorrência com banco em Testcontainers, API black-box, integração e JMeter após metas aprovadas. Nenhum mecanismo técnico específico é prescrito.

#### Critérios de sucesso

Exatamente uma reserva aceita, outra tentativa recusada, banco consistente e conflito evitado disponível para relatório quando a fórmula for definida.

#### Pendências

Limites de intervalo, alterações concorrentes, cancelamento concorrente e ocupação de `SOLICITADA`.

### FLX-07: Aprovação de recurso restrito

#### Objetivo

Permitir ao Responsável decidir sobre solicitação especial sem aceitar conflito ou contornar autorização.

#### Personas participantes

- **Persona principal:** Responsável.
- **Personas de apoio:** Solicitante acompanha resultado; Administrador mantém recursos.
- **Sem permissão:** Solicitante e Administrador não aprovam.

#### Gatilho

Existe solicitação especial de recurso restrito em `SOLICITADA`.

#### Pré-condições

Responsável autenticado e autorizado para a solicitação; disponibilidade pode ter mudado desde a criação.

#### Dados necessários

Solicitação, recurso, período, Solicitante, disponibilidade, agenda docente, bloqueio e manutenção.

#### Fluxo principal

1. Responsável consulta a solicitação; sistema valida perfil e responsabilidade; aplica RN-06.
2. Sistema revalida disponibilidade, conflito, agenda docente, bloqueio e manutenção antes da decisão; aplica RN-02, RN-03 e RN-05.
3. Responsável aprova quando as regras são atendidas; sistema altera para `APROVADA` conforme o fluxo oficial; aplica RN-07 e RN-09.
4. Sistema produz auditoria; notificação depende da decisão de integração.

#### Fluxos alternativos

Responsável rejeita a solicitação; sistema usa estado `REJEITADA`, registra auditoria e libera o prosseguimento conforme regra de disponibilidade ainda pendente.

#### Fluxos de exceção

Perfil indevido, solicitação fora da responsabilidade, conflito novo, manutenção, bloqueio, solicitação já decidida ou estado inválido resultam em recusa controlada.

#### Pós-condições

Solicitação fica `APROVADA` ou `REJEITADA`, sem aprovação por Solicitante/Admin e sem conflito aceito.

#### Regras de negócio relacionadas

RN-02, RN-03, RN-05, RN-06, RN-07 e RN-09.

#### Requisitos relacionados

RF-01, RF-14, RF-15, RF-18, RF-19, RF-20, RNF-08, RNF-15.

#### Auditoria esperada

Autor, decisão, estado anterior/posterior e entidade afetada devem ser auditáveis; campos mínimos ainda pendentes.

#### Notificações esperadas

Resultado para Solicitante e demais destinatários somente após definição de evento e canal.

#### Evidências e testes sugeridos

API e integração, testes positivos/negativos de autorização, Testcontainers para persistência/auditoria, E2E e WireMock.

#### Critérios de sucesso

Somente Responsável autorizado aprova, disponibilidade é revalidada, conflito impede aprovação, estado e decisão são auditados.

#### Pendências

Definição de recurso restrito, solicitação especial, responsabilidade, justificativa e aprovação após mudança de disponibilidade.

### FLX-08: Alteração de reserva

#### Objetivo

Permitir alteração de reserva própria antes do início, com nova validação e rastreabilidade.

#### Personas participantes

- **Persona principal:** Solicitante proprietário.
- **Personas de apoio:** Responsável pode participar se nova aprovação for exigida; Administrador mantém indisponibilidades.
- **Sem permissão:** Solicitante de terceiro, Responsável fora da regra e Administrador não alteram reserva como atalho não definido.

#### Gatilho

Solicitante solicita alteração de sua reserva.

#### Pré-condições

Reserva pertence ao Solicitante, não foi iniciada e dados novos estão disponíveis.

#### Dados necessários

Reserva, novos recursos ou período, proprietário e estado atual.

#### Fluxo principal

1. Solicitante seleciona sua reserva; sistema valida propriedade e estado; aplica RN-08.
2. Sistema valida término posterior ao início, sobreposição em todos os recursos, agenda docente, bloqueio e manutenção; aplica RN-01, RN-02, RN-03 e RN-05.
3. Sistema verifica concorrência da alteração; regra detalhada é pendente, mas não pode gerar inconsistência.
4. Sistema salva alteração permitida e gera auditoria; se houver recurso restrito, nova aprovação é pendente de decisão.

#### Fluxos alternativos

Alteração somente de período ou de recurso, sempre com nova validação aplicável.

#### Fluxos de exceção

Reserva de terceiro, iniciada, `CONCLUIDA`, `REJEITADA` ou `CANCELADA`, conflito, manutenção, bloqueio, dados inválidos ou transição não definida devem ser recusados ou marcados como pendência.

#### Pós-condições

Reserva própria é atualizada sem conflito, ou permanece sem alteração.

#### Regras de negócio relacionadas

RN-01, RN-02, RN-03, RN-05, RN-08 e RN-09.

#### Requisitos relacionados

RF-11, RF-13, RF-18, RF-19, RNF-07, RNF-09, RNF-15.

#### Auditoria esperada

Alteração efetivada e mudança de estado, quando houver, devem ser auditáveis.

#### Notificações esperadas

Resultado da alteração e eventual nova aprovação, se definidos.

#### Evidências e testes sugeridos

JUnit 5 parametrizado, API, integração com Testcontainers, autorização, concorrência da alteração e auditoria.

#### Critérios de sucesso

Somente proprietário autorizado altera reserva não iniciada; todos os recursos são revalidados; não há conflito; aprovação anterior não é presumida como válida após troca de recurso.

#### Pendências

Estados alteráveis, alteração de recurso restrito, alteração de professor validado, concorrência e permissão administrativa corretiva.

### FLX-09: Cancelamento

#### Objetivo

Cancelar reserva própria permitida, alterando-a para `CANCELADA` sem excluir histórico.

#### Personas participantes

- **Persona principal:** Solicitante proprietário.
- **Personas de apoio:** Responsável ou Administrador somente conforme regra futura, sem permissão presumida.
- **Sem permissão:** usuário de outro perfil ou proprietário de outra reserva.

#### Gatilho

Solicitante solicita cancelamento.

#### Pré-condições

Reserva pertence ao Solicitante e não foi iniciada, conforme regra documentada.

#### Dados necessários

Reserva, proprietário e estado atual.

#### Fluxo principal

1. Solicitante solicita cancelamento; sistema valida propriedade e estado; aplica RN-08.
2. Sistema altera para `CANCELADA`; aplica RN-07 e RN-09; preserva histórico.
3. Sistema avalia liberação da disponibilidade conforme política pendente e produz auditoria.

#### Fluxos alternativos

Cancelamento de uma reserva não iniciada em estado oficialmente permitido, somente após a equipe definir os estados de origem.

#### Fluxos de exceção

Reserva iniciada, de terceiro, estado não permitido ou falha de persistência resultam em recusa sem exclusão.

#### Pós-condições

Reserva permanece registrada como `CANCELADA`; liberação do recurso e efeito em relatórios aguardam definição.

#### Regras de negócio relacionadas

RN-07, RN-08 e RN-09.

#### Requisitos relacionados

RF-12, RF-18, RF-19, RF-20, RNF-07, RNF-15.

#### Auditoria esperada

Mudança para `CANCELADA` deve ser registrada; histórico não é apagado.

#### Notificações esperadas

Notificação de cancelamento é dependente de canal e evento aprovados.

#### Evidências e testes sugeridos

API, autorização positiva/negativa, integração com Testcontainers e E2E de histórico.

#### Critérios de sucesso

Proprietário cancela somente quando permitido, estado é `CANCELADA`, histórico permanece e reserva iniciada não é apagada.

#### Pendências

Estados de origem, motivo, liberação, cancelamento durante concorrência e cancelamento após retirada.

### FLX-10: Início da utilização

#### Objetivo

Representar o início efetivo de uso como `EM_USO` sem apagar a reserva iniciada.

#### Personas participantes

- **Persona principal:** perfil que for definido pela equipe.
- **Personas de apoio:** Solicitante utiliza; Responsável pode acompanhar retirada.
- **Sem permissão:** nenhum perfil pode ser atribuído por inferência.

#### Gatilho

Momento de início da utilização da reserva.

#### Pré-condições

Reserva em estado compatível, aprovação quando aplicável e data/período correspondente.

#### Dados necessários

Reserva, estado atual, momento de início e recursos associados.

#### Fluxo principal

1. Sistema ou perfil autorizado tenta iniciar uso; valida estado, autorização e condições; transição para `EM_USO` é a etapa oficial, mas ator e momento são pendentes.
2. Sistema registra auditoria da mudança; impede apagamento posterior pela RN-08.
3. Retirada de material pode ser registrada em fluxo próprio; relação obrigatória com `EM_USO` é pendente.

#### Fluxos alternativos

A equipe pode definir início automático ou registro por perfil, mas ambas são opções não aprovadas.

#### Fluxos de exceção

Estado incompatível, autorização ausente, período inválido ou tentativa de apagar reserva iniciada são recusados.

#### Pós-condições

Reserva fica `EM_USO` somente quando a transição for aprovada e registrada.

#### Regras de negócio relacionadas

RN-07, RN-08 e RN-09.

#### Requisitos relacionados

RF-18, RF-19, RF-22, RNF-15.

#### Auditoria esperada

Mudança para `EM_USO`, autor e momento devem ser auditáveis.

#### Notificações esperadas

Evento e destinatários pendentes.

#### Evidências e testes sugeridos

JUnit 5 parametrizado de transições, API de autorização, integração com Testcontainers e E2E.

#### Critérios de sucesso

A transição oficial é respeitada, auditoria é gerada e a reserva iniciada não pode ser apagada.

#### Pendências

Quem inicia, quando inicia, relação com retirada e permissões por estado.

### FLX-11: Retirada de material

#### Objetivo

Registrar e acompanhar a retirada de material ou equipamento associado a uma reserva.

#### Personas participantes

- **Persona principal:** Responsável.
- **Personas de apoio:** Solicitante acompanha conforme autorização; Administrador consulta conforme escopo.
- **Sem permissão:** Solicitante não registra retirada.

#### Gatilho

Material ou equipamento associado a uma reserva precisa ser retirado.

#### Pré-condições

Responsável autenticado; reserva e material/equipamento associados; condição temporal/estado aplicável ainda pendente.

#### Dados necessários

Reserva, material ou equipamento, Responsável e momento da retirada.

#### Fluxo principal

1. Responsável localiza a reserva e material; sistema valida autorização e associação; aplica escopo E7.
2. Responsável registra retirada; sistema persiste e vincula o registro; auditoria de movimentação é conforme política.
3. Sistema permite acompanhamento; impacto no estado da reserva é pendente.

#### Fluxos alternativos

Acompanhamento de retirada já registrada.

#### Fluxos de exceção

Reserva/material inexistente, perfil indevido, retirada duplicada ou estado incompatível são recusados conforme regras definidas.

#### Pós-condições

Retirada registrada e disponível para acompanhamento.

#### Regras de negócio relacionadas

RN-09 e fluxo de estados oficial quando aplicável.

#### Requisitos relacionados

RF-16, RF-18, RF-19, RNF-07, RNF-15.

#### Auditoria esperada

Registro da retirada, autor, momento e entidade afetada; conteúdo mínimo pendente.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Integração com Testcontainers, API de autorização, E2E e testes parametrizados de associação.

#### Critérios de sucesso

Somente Responsável registra retirada associada a reserva; registro fica persistido, acompanhável e rastreável.

#### Pendências

Momento permitido, condição do material, retirada parcial/duplicada e perfil com responsabilidade específica.

### FLX-12: Devolução de material

#### Objetivo

Registrar a devolução correspondente à retirada e acompanhar o encerramento da movimentação.

#### Personas participantes

- **Persona principal:** Responsável.
- **Personas de apoio:** Solicitante acompanha conforme autorização; Administrador consulta conforme escopo.
- **Sem permissão:** perfis sem permissão de registro.

#### Gatilho

Material retirado deve ser devolvido.

#### Pré-condições

Responsável autenticado e retirada correspondente registrada.

#### Dados necessários

Retirada, reserva, material/equipamento e momento da devolução.

#### Fluxo principal

1. Responsável localiza retirada; sistema valida associação e autorização; aplica E7.
2. Responsável registra devolução; sistema grava vínculo e auditoria aplicável.
3. Sistema disponibiliza acompanhamento; liberação do recurso e conclusão são pendentes quando não houver regra.

#### Fluxos alternativos

Consulta ou acompanhamento de devolução já registrada.

#### Fluxos de exceção

Sem retirada correspondente, devolução duplicada, recurso inexistente, perfil indevido ou estado incompatível resultam em recusa controlada.

#### Pós-condições

Devolução registrada e associada à retirada.

#### Regras de negócio relacionadas

RN-09.

#### Requisitos relacionados

RF-17, RF-19, RNF-07, RNF-15.

#### Auditoria esperada

Registro da devolução, autor, momento e entidade afetada conforme política.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Integração com Testcontainers, API, autorização, E2E e teste negativo sem retirada.

#### Critérios de sucesso

Devolução só é registrada com retirada correspondente e permanece acompanhável.

#### Pendências

Condição, atraso, divergência, efeito sobre disponibilidade e se devolução é pré-condição de `CONCLUIDA`.

### FLX-13: Conclusão da reserva

#### Objetivo

Representar a conclusão como `CONCLUIDA` preservando auditoria e atualizando os dados operacionais.

#### Personas participantes

- **Persona principal:** perfil que for autorizado pela equipe.
- **Personas de apoio:** Responsável acompanha devolução; Administrador consulta relatórios; Solicitante consulta resultado.
- **Sem permissão:** não se presume perfil para concluir.

#### Gatilho

Uso da reserva termina e as condições de conclusão são avaliadas.

#### Pré-condições

Reserva em `EM_USO`; critérios de conclusão e devolução ainda não definidos.

#### Dados necessários

Reserva, estado atual, movimentações de material e momento da conclusão.

#### Fluxo principal

1. Perfil autorizado verifica validações; sistema checa estado e movimentações conforme regras aprovadas.
2. Sistema altera `EM_USO` para `CONCLUIDA`; aplica RN-07 e RN-09.
3. Sistema registra auditoria e atualiza relatórios; liberação do recurso é pendente.

#### Fluxos alternativos

Conclusão sem material associado, se a equipe aprovar essa condição; não é regra atual.

#### Fluxos de exceção

Estado incorreto, devolução pendente, autorização ausente ou tentativa de transição não definida resultam em recusa ou pendência.

#### Pós-condições

Reserva `CONCLUIDA` e mudança auditada, se a transição for executada.

#### Regras de negócio relacionadas

RN-07 e RN-09.

#### Requisitos relacionados

RF-18, RF-19, RF-21, RNF-04, RNF-07.

#### Auditoria esperada

Transição para `CONCLUIDA` e dados da operação devem ser auditáveis.

#### Notificações esperadas

Evento e destinatários pendentes.

#### Evidências e testes sugeridos

JUnit 5 de transições, Testcontainers, API e E2E com devolução pendente e concluída.

#### Critérios de sucesso

Somente transição autorizada chega a `CONCLUIDA`, auditoria é criada e relatório recebe o evento conforme fórmula aprovada.

#### Pendências

Perfil, momento, validações, devolução obrigatória e liberação de recursos.

### FLX-14: Rejeição

#### Objetivo

Registrar a rejeição de solicitação especial como `REJEITADA` somente por perfil autorizado.

#### Personas participantes

- **Persona principal:** Responsável.
- **Personas de apoio:** Solicitante recebe o resultado; Administrador sustenta cadastro.
- **Sem permissão:** Solicitante e Administrador não rejeitam em lugar do Responsável.

#### Gatilho

Responsável decide não aprovar solicitação especial.

#### Pré-condições

Solicitação pendente, recurso restrito e Responsável autorizado.

#### Dados necessários

Solicitação, recurso, estado, Responsável e motivo, sendo motivo obrigatório pendente.

#### Fluxo principal

1. Responsável consulta e valida a solicitação; sistema confirma autorização e estado.
2. Responsável rejeita; sistema muda para `REJEITADA`; aplica RN-07 e RN-09.
3. Sistema registra auditoria; efeito na disponibilidade e notificação permanecem pendentes.

#### Fluxos alternativos

Nenhum fluxo adicional é aprovado pela fonte.

#### Fluxos de exceção

Acesso indevido, solicitação já decidida, conflito ou estado incompatível impedem a rejeição.

#### Pós-condições

Solicitação `REJEITADA`, sem apagar histórico.

#### Regras de negócio relacionadas

RN-06, RN-07 e RN-09.

#### Requisitos relacionados

RF-14, RF-18, RF-19, RF-20.

#### Auditoria esperada

Autor, estado anterior/posterior e decisão devem ser auditáveis.

#### Notificações esperadas

Notificação ao Solicitante é pendente de definição.

#### Evidências e testes sugeridos

API, autorização positiva/negativa, integração e E2E com auditoria.

#### Critérios de sucesso

Somente Responsável autorizado rejeita, estado é `REJEITADA`, histórico é preservado e decisão é auditável.

#### Pendências

Motivo obrigatório, liberação, reabertura e transições seguintes.

### FLX-15: Não comparecimento

#### Objetivo

Documentar o estado oficial `NAO_COMPARECEU` sem inventar sua origem ou responsável.

#### Personas participantes

- **Persona principal:** PENDENTE DE DECISÃO DA EQUIPE.
- **Personas de apoio:** Solicitante, Responsável e Administrador podem ser afetados.
- **Sem permissão:** não se atribui operação a qualquer perfil por inferência.

#### Gatilho

Possível ausência na utilização da reserva, sem regra oficial de registro.

#### Pré-condições

Reserva existente e condição de não comparecimento identificada, sem tolerância ou momento definidos.

#### Dados necessários

Reserva, estado, evento de ausência, autor e momento, todos com detalhes pendentes.

#### Fluxo principal

1. Sistema ou perfil ainda não definido identifica possível não comparecimento; validação e autorização são pendentes.
2. Caso a equipe aprove a transição, reserva passa a `NAO_COMPARECEU`; RN-07 e RN-09 se aplicam.
3. Sistema audita o evento; disponibilidade, notificação e relatório aguardam definição.

#### Fluxos alternativos

Nenhum fluxo alternativo é oficial.

#### Fluxos de exceção

Tentativa por perfil não definido, momento não aprovado ou transição inválida não deve alterar dados.

#### Pós-condições

Somente após decisão: estado `NAO_COMPARECEU` e auditoria correspondente.

#### Regras de negócio relacionadas

RN-07 e RN-09.

#### Requisitos relacionados

RF-18, RF-19, RF-21, RF-20.

#### Auditoria esperada

Se efetivada, a mudança deve ser auditada.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Testes parametrizados de transição após aprovação das regras; API negativa para transição não definida.

#### Critérios de sucesso

Nenhuma origem, ator ou tolerância é inventada; o estado somente é usado após decisão da equipe.

#### Pendências

Todas as dúvidas listadas na seção 16, especialmente origem, perfil, momento e efeitos.

### FLX-16: Bloqueio de recurso

#### Objetivo

Gerenciar bloqueio de recurso e impedir reserva no período bloqueado.

#### Personas participantes

- **Persona principal:** Administrador.
- **Personas de apoio:** Solicitante pesquisa disponibilidade; Responsável consulta quando necessário.
- **Sem permissão:** Solicitante e Responsável não gerenciam bloqueios.

#### Gatilho

Administrador precisa tornar recurso indisponível durante um período.

#### Pré-condições

Administrador autenticado e recurso cadastrado.

#### Dados necessários

Recurso, período do bloqueio e estado; motivo e demais campos não especificados.

#### Fluxo principal

1. Administrador cria ou altera bloqueio; sistema valida autorização e entrada; aplica escopo E6.
2. Sistema considera o bloqueio na pesquisa e disponibilidade; aplica RN-05.
3. Tentativa de reserva no período é recusada; registra auditoria conforme política.
4. Encerramento do bloqueio altera disponibilidade; momento e efeito são pendentes.

#### Fluxos alternativos

Consulta de bloqueio e encerramento quando suportados pela decisão da equipe.

#### Fluxos de exceção

Recurso inexistente, período inválido, conflito com reserva existente ou acesso indevido resultam em recusa ou pendência sem regra inventada.

#### Pós-condições

Recurso não aparece como disponível no período bloqueado, após comportamento aprovado.

#### Regras de negócio relacionadas

RN-05 e RN-09.

#### Requisitos relacionados

RF-06, RF-09, RF-10, RF-19, RNF-15.

#### Auditoria esperada

Criação, alteração e encerramento conforme política; mudanças de estado de reserva sempre auditadas.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

API, integração com Testcontainers, parametrizados de períodos e E2E de pesquisa/reserva.

#### Critérios de sucesso

Administrador gerencia o bloqueio, pesquisa o considera e reserva no período bloqueado é impedida.

#### Pendências

Relação com manutenção, bloqueio parcial/recorrente, reservas existentes, encerramento e liberação.

### FLX-17: Manutenção

#### Objetivo

Registrar período de manutenção e impedir reserva de recurso em manutenção.

#### Personas participantes

- **Persona principal:** Administrador.
- **Personas de apoio:** Solicitante pesquisa e tenta reservar; Responsável é afetado em aprovação.
- **Sem permissão:** Solicitante e Responsável não gerenciam manutenção.

#### Gatilho

Administrador precisa registrar manutenção de recurso.

#### Pré-condições

Recurso cadastrado e Administrador autenticado.

#### Dados necessários

Recurso, período de manutenção e situação; campos adicionais não definidos.

#### Fluxo principal

1. Administrador cria ou atualiza período; sistema valida autorização e entrada; aplica E6.
2. Pesquisa informa indisponibilidade; aplica RN-05.
3. Tentativa de reserva é recusada; sistema apresenta mensagem compreensível.
4. Alteração/encerramento da manutenção atualiza disponibilidade conforme regra pendente.

#### Fluxos alternativos

Consulta de manutenção e encerramento quando definidos.

#### Fluxos de exceção

Dados inválidos, recurso inexistente, acesso indevido ou manutenção sobre reserva existente são tratados sem escolher cancelamento, rejeição ou manutenção da reserva.

#### Pós-condições

Recurso em manutenção não pode ser reservado.

#### Regras de negócio relacionadas

RN-05 e RN-09.

#### Requisitos relacionados

RF-07, RF-09, RF-10, RF-11, RF-19, RNF-15, RNF-17.

#### Auditoria esperada

Manutenção e seus efeitos devem ser auditáveis conforme política; mudança de estado de reserva é sempre auditada.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Testcontainers, API, E2E, parametrizados de períodos e validação negativa de reserva.

#### Critérios de sucesso

Período é gerenciado pelo Administrador, pesquisa reflete indisponibilidade e reserva é impedida.

#### Pendências

Tratamento de reservas existentes, retroatividade, relação com bloqueio e encerramento.

### FLX-18: Auditoria

#### Objetivo

Preservar histórico auditável de mudanças e eventos relevantes.

#### Personas participantes

- **Persona principal:** sistema registra; autor é Solicitante, Responsável, Administrador ou processo automático conforme evento.
- **Personas de apoio:** Administrador consulta histórico; demais perfis consultam somente se autorizados.
- **Sem permissão:** perfis não autorizados não consultam nem alteram registros.

#### Gatilho

Mudança de estado ou operação definida como auditável ocorre.

#### Pré-condições

Operação autorizada ou processo automático aplicável.

#### Dados necessários

Ação, autor, data/hora, entidade afetada, estado anterior, estado posterior e dados alterados, sujeitos à política de minimização e definição da equipe.

#### Fluxo principal

1. Persona ou processo executa mudança; sistema valida operação; aplica RN-09.
2. Sistema registra auditoria vinculada à entidade e mudança; estado é atualizado quando aplicável.
3. Perfil autorizado consulta o histórico; sistema aplica autorização; não permite alteração operacional do registro.

#### Fluxos alternativos

Auditoria de aprovação, rejeição, criação, alteração, cancelamento, bloqueio, manutenção, retirada e devolução se a equipe as classificar como auditáveis.

#### Fluxos de exceção

Falha de persistência, acesso indevido, tentativa de alterar histórico ou operação parcialmente falha devem ser tratados conforme política ainda não definida.

#### Pós-condições

Mudança de estado possui registro de auditoria; demais operações dependem da política aprovada.

#### Regras de negócio relacionadas

RN-09 e RN-10.

#### Requisitos relacionados

RF-19, RNF-04, RNF-06, RNF-07, RNF-18.

#### Auditoria esperada

O próprio evento de auditoria deve ser rastreável sem armazenar dados sensíveis desnecessários.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Testcontainers, integração transacional, API de consulta/autorização, E2E e inspeção documental.

#### Critérios de sucesso

Toda mudança de estado possui autor e registro consultável; registros não são alterados por perfis operacionais.

#### Pendências

Campos mínimos, retenção, visibilidade por perfil, tentativas recusadas, falha parcial e política de imutabilidade.

### FLX-19: Notificação

#### Objetivo

Produzir notificação simulada ou realizar integração com API externa para evento aprovado.

#### Personas participantes

- **Persona principal:** processo de notificação ou integração.
- **Personas de apoio:** Solicitante, Responsável e Administrador recebem conforme evento e autorização.
- **Sem permissão:** nenhum perfil deve acessar dados de destinatário fora da política.

#### Gatilho

Evento de reserva, aprovação, rejeição, cancelamento ou movimentação que venha a ser escolhido pela equipe.

#### Pré-condições

Alternativa de notificação simulada ou API externa definida.

#### Dados necessários

Evento, entidade, estado, destinatário e conteúdo, ainda não especificados.

#### Fluxo principal

1. Sistema identifica evento definido; valida dados e autorização; aplica escopo E9.
2. Produz notificação simulada ou chamada externa; registra resultado sem expor dados indevidos.
3. Operação principal mantém consistência quando a integração falha, conforme política a decidir; erro fica observável.

#### Fluxos alternativos

Notificação simulada ou integração externa com WireMock nos testes.

#### Fluxos de exceção

Timeout, erro 4xx/5xx, resposta inválida, indisponibilidade e repetição devem ser tratados de forma segura, sem presumir retry ou idempotência.

#### Pós-condições

Notificação ou chamada produzida quando configurada; falha não deve corromper a reserva.

#### Regras de negócio relacionadas

RN-06, RN-07 e RN-09.

#### Requisitos relacionados

RF-20, RF-14, RF-12, RF-19, RNF-08, RNF-15.

#### Auditoria esperada

Resultado e falha da integração podem ser auditados conforme política.

#### Notificações esperadas

A própria notificação é o resultado; canal, evento, destinatário e conteúdo permanecem pendentes.

#### Evidências e testes sugeridos

WireMock para sucesso, erro, timeout e resposta inválida; integração, API e E2E. Nenhuma integração real foi executada.

#### Critérios de sucesso

Alternativa escolhida produz resultado observável, falha é tratada com segurança e operação principal mantém consistência.

#### Pendências

Escolha de alternativa, canal, destinatários, eventos, conteúdo, retry e isolamento da falha.

### FLX-20: Relatórios

#### Objetivo

Disponibilizar utilização por recurso, carga horária alocada e conflitos evitados.

#### Personas participantes

- **Persona principal:** Administrador.
- **Personas de apoio:** sistema consolida reservas e conflitos; demais perfis consultam somente se autorizados.
- **Sem permissão:** Solicitante não possui permissão definida para relatório operacional na persona; acesso é tratado como negado até decisão.

#### Gatilho

Administrador consulta relatório operacional.

#### Pré-condições

Administrador autenticado; dados de reservas e conflitos disponíveis.

#### Dados necessários

Recurso, reservas, períodos, carga horária e registros de conflitos evitados. Fórmulas e filtros não definidos.

#### Fluxo principal

1. Administrador solicita relatório; sistema valida autorização e filtros disponíveis; aplica E10.
2. Sistema consolida utilização, carga horária e conflitos evitados sem inventar fórmula; valida consistência.
3. Sistema apresenta resultado e preserva rastreabilidade da consulta conforme política.

#### Fluxos alternativos

Consulta por recurso ou período somente quando filtros forem aprovados.

#### Fluxos de exceção

Sem dados, filtro inválido, perfil indevido ou cálculo não definido resultam em mensagem compreensível e sem dado inventado.

#### Pós-condições

Relatório observável ou erro controlado; dados de reserva não são alterados.

#### Regras de negócio relacionadas

RN-02, RN-03, RN-04 e RN-10.

#### Requisitos relacionados

RF-21, RNF-14, RNF-17, RNF-18.

#### Auditoria esperada

Consulta pode ser auditada conforme política, sem presumir retenção.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

API, integração com dados controlados, E2E, JMeter após aprovação de metas e comparação documental.

#### Critérios de sucesso

Os três indicadores oficiais são apresentados sem fórmula inventada e somente a perfis autorizados.

#### Pendências

Fórmula de conflitos evitados, filtros, período, agrupamento, formato e perfis de consulta.

### FLX-21: Erros e mensagens

#### Objetivo

Comunicar recusas e falhas de forma compreensível, segura e observável.

#### Personas participantes

- **Persona principal:** qualquer persona que recebe erro em operação própria.
- **Personas de apoio:** sistema aplica autorização e validação.
- **Sem permissão:** operação recusada não deve alterar dados.

#### Gatilho

Entrada inválida, conflito, indisponibilidade, acesso negado, manutenção, bloqueio, falha externa ou erro interno.

#### Pré-condições

Uma operação ou requisição foi recebida.

#### Dados necessários

Tipo de erro e contexto mínimo necessário para informar o motivo sem dados sensíveis.

#### Fluxo principal

1. Sistema valida entrada e operação; identifica falha; aplica regra correspondente.
2. Sistema recusa ou informa resultado parcial conforme regra aprovada; não expõe stack trace, credenciais, detalhes internos, caminhos, SQL ou dados sensíveis.
3. Persona recebe mensagem compreensível; auditoria da tentativa depende da política.

#### Fluxos alternativos

Mensagens específicas para período inválido, conflito, recurso indisponível, manutenção, bloqueio, autorização e integração.

#### Fluxos de exceção

Erro interno não tratado, payload inválido ou falha de integração devem retornar resposta segura e preservar consistência.

#### Pós-condições

Usuário compreende o motivo observável; dados não são alterados indevidamente.

#### Regras de negócio relacionadas

RN-01, RN-02, RN-05, RN-06 e RN-08.

#### Requisitos relacionados

RF-01, RF-09, RF-10, RF-11, RF-12, RF-22, RNF-06, RNF-15, RNF-17.

#### Auditoria esperada

Erros efetivos e tentativas recusadas seguem política ainda pendente.

#### Notificações esperadas

Não confundidas com mensagens de erro; canal de notificação permanece pendente.

#### Evidências e testes sugeridos

API black-box, testes de validação, autorização, E2E, SonarCloud e revisão de segurança.

#### Critérios de sucesso

Erros são compreensíveis, não expõem detalhes internos e não deixam alteração inconsistente.

#### Pendências

Códigos HTTP, formato de erro, correlação, catálogo de mensagens e escopo de fluxo crítico.

### FLX-22: Documentação da API ou fluxos públicos

#### Objetivo

Documentar contratos ou fluxos públicos, incluindo autenticação, autorização, entradas, respostas e erros.

#### Personas participantes

- **Persona principal:** equipe do sistema como responsável pela documentação.
- **Personas de apoio:** Solicitante, Responsável e Administrador são usuários dos fluxos documentados.
- **Sem permissão:** documentação não concede autorização operacional.

#### Gatilho

API ou fluxo público é definido ou alterado.

#### Pré-condições

Fluxos públicos e operações existentes identificados.

#### Dados necessários

Operação, autenticação, perfis autorizados, entradas, resposta, estados e erros.

#### Fluxo principal

1. Equipe documenta operação ou fluxo; valida aderência ao PRD e aos estados oficiais.
2. Documenta autorizações, erros e exemplos consistentes; não inventa transições ou dados.
3. Revisa a documentação contra API ou fluxo público e registra evidência de inspeção.

#### Fluxos alternativos

Documentar API ou documentar fluxos públicos, conforme escolha da equipe.

#### Fluxos de exceção

Divergência entre documento e comportamento, exemplo inconsistente ou operação não definida exige correção ou pendência.

#### Pós-condições

Usuário consegue consultar a documentação correspondente aos fluxos públicos escolhidos.

#### Regras de negócio relacionadas

RN-06, RN-07 e RN-09.

#### Requisitos relacionados

RF-23, RNF-18.

#### Auditoria esperada

Alterações documentais podem ser versionadas conforme processo da equipe; não há política oficial adicional.

#### Notificações esperadas

Não definidas.

#### Evidências e testes sugeridos

Inspeção documental, API black-box ou execução do fluxo público documentado e revisão cruzada.

#### Critérios de sucesso

Autenticação, perfis, entradas, respostas, erros, estados e operações públicas escolhidas estão descritos sem divergência.

#### Pendências

Escolha entre API e fluxos públicos, formato, escopo exato e mecanismo de publicação.

## 8. Cenários Integrados

### Cenário A: reserva válida de recurso não restrito

1. Administrador cadastra sala, professor, material ou equipamento e mantém o recurso fora de bloqueio/manutenção.
2. Solicitante pesquisa filtros e disponibilidade; sistema considera reservas, agenda docente, bloqueio e manutenção.
3. Solicitante envia período com término posterior ao início.
4. Sistema valida sala, material, equipamento e professor e registra a solicitação.
5. O estado inicial de reserva não restrita e o ponto de aprovação são `PENDENTE DE DECISÃO DA EQUIPE`.
6. Uso, conclusão, auditoria e liberação seguem os estados oficiais e as transições ainda não definidas.

### Cenário B: reserva de recurso restrito

1. Administrador cadastra/configura o recurso.
2. Solicitante pesquisa e solicita a reserva.
3. Sistema registra `SOLICITADA` e revalida conflitos, agenda docente, bloqueio e manutenção.
4. Responsável analisa e aprova; sistema muda para `APROVADA` e audita.
5. A passagem para `EM_USO` depende do momento e perfil ainda não definidos.
6. Responsável acompanha/Registra retirada, devolução e eventual conclusão conforme regras pendentes.
7. Notificações e liberação seguem decisão da equipe.

### Cenário C: rejeição de recurso restrito

1. Solicitante cria a solicitação.
2. Responsável consulta, verifica dados e rejeita dentro de sua responsabilidade.
3. Sistema muda para `REJEITADA`, preserva o histórico e audita.
4. Liberação do recurso e notificação são pendentes.

### Cenário D: conflito na agenda do professor

1. Solicitante seleciona professor como recurso.
2. Existe reserva na agenda do professor no período.
3. Sistema detecta sobreposição mesmo que sala/material estejam livres.
4. Solicitação é recusada com mensagem compreensível e sem reserva inconsistente.
5. Conflito evitado pode alimentar relatório, mas sua fórmula é pendente.

### Cenário E: duas solicitações simultâneas

1. Dois Solicitantes enviam o mesmo recurso e período.
2. Sistema valida concorrência e mantém consistência.
3. Somente uma reserva é aceita; outra é recusada com conflito.
4. Resultado é auditável conforme política e deve servir como evidência de teste automatizado.

### Cenário F: recurso em manutenção

1. Administrador registra manutenção do recurso.
2. Solicitante pesquisa e recebe indisponibilidade.
3. Tentativa de reserva é recusada com mensagem compreensível.
4. Auditoria da manutenção e da tentativa segue política; reservas existentes e liberação são pendentes.

### Cenário G: cancelamento

1. Existe reserva própria não iniciada.
2. Solicitante é autenticado e tem propriedade validada.
3. Sistema muda para `CANCELADA`, preserva histórico e audita.
4. Liberação do recurso, notificação e relatórios dependem de decisão.

### Cenário H: retirada e devolução

1. Reserva aprovada chega ao uso quando a transição for definida.
2. Responsável registra retirada vinculada à reserva.
3. Responsável acompanha e registra devolução correspondente.
4. Conclusão, liberação e relação com devolução permanecem pendentes quando não definidas.
5. Cada mudança de estado efetivada é auditada.

### Cenário I: tentativa de ação sem autorização

1. Solicitante tenta aprovar recurso restrito; sistema recusa no back-end.
2. Responsável tenta gerir sala, usuário ou manutenção; sistema recusa.
3. Usuário acessa diretamente operação sem permissão; sistema recusa sem alterar dados.
4. Mensagem é segura e compreensível; tentativa e auditoria seguem política.

## 9. Jornada Resumida por Persona

### Solicitante

Autenticar -> consultar recursos -> aplicar filtros -> verificar sala/material/professor e agenda -> informar período -> criar solicitação -> aguardar aprovação se aplicável -> acompanhar estado -> utilizar quando autorizado -> alterar ou cancelar se permitido -> consultar resultado e histórico.

### Responsável

Autenticar -> consultar solicitação especial -> verificar Solicitante, recurso, disponibilidade, agenda, manutenção e bloqueio -> aprovar ou rejeitar -> auditar decisão -> validar docente -> acompanhar retirada -> registrar/acompanhar devolução -> consultar histórico e conclusão quando autorizada.

### Administrador

Autenticar -> gerenciar usuários/perfis -> cadastrar e atualizar recursos -> criar/alterar/encerrar bloqueios e manutenção conforme decisões -> verificar impacto na disponibilidade -> consultar histórico -> consultar utilização, carga horária e conflitos evitados -> preservar autorização e regras críticas.

## 10. Matriz de Participação

| Fluxo | Solicitante | Responsável | Administrador | Regra principal | Estado afetado | Auditoria |
|---|---|---|---|---|---|---|
| FLX-01 | Executa acesso próprio | Executa acesso próprio | Executa e gerencia usuários | Autorização por perfil | Nenhum | Conforme política |
| FLX-02 | Consulta | Consulta quando necessário | Gerencia | Cadastro autorizado | Nenhum | Alterações conforme política |
| FLX-03 | Recebe perfil | Recebe perfil | Gerencia | Somente três perfis | Nenhum | Alterações conforme política |
| FLX-04 | Executa pesquisa | Consulta quando autorizado | Mantém dados | Manutenção/bloqueio/conflito excluem disponibilidade | Nenhum | Conforme política |
| FLX-05 | Executa própria solicitação | Recebe para aprovação se restrita | Prepara recursos | Sem sobreposição e aprovação restrita | `SOLICITADA` ou pendente | Mudanças de estado |
| FLX-06 | Participa da concorrência | Sem ação principal | Consulta evidência | Uma aceita | Reserva | Conforme política |
| FLX-07 | Recebe decisão | Aprova/rejeita | Não substitui | Somente Responsável aprova | `SOLICITADA` -> `APROVADA`/`REJEITADA` | Obrigatória na mudança |
| FLX-08 | Altera própria se permitido | Apoia se nova aprovação for definida | Mantém indisponibilidade | Revalidar conflito | Pendente | Alteração/mudança de estado |
| FLX-09 | Cancela própria se permitido | Pendente | Pendente | Reserva iniciada não pode ser apagada | `CANCELADA` | Obrigatória na mudança |
| FLX-10 | Utiliza | Acompanha | Consulta | Transição pendente | `EM_USO` | Obrigatória |
| FLX-11 | Acompanha | Registra | Consulta | Retirada associada | Pendente | Conforme política |
| FLX-12 | Acompanha | Registra | Consulta | Devolução exige retirada | Pendente | Conforme política |
| FLX-13 | Consulta | Acompanha | Consulta relatório | Transição pendente | `CONCLUIDA` | Obrigatória |
| FLX-14 | Recebe decisão | Rejeita | Não substitui | Recurso restrito | `REJEITADA` | Obrigatória |
| FLX-15 | Afetado | Afetado | Afetado | Perfil e origem pendentes | `NAO_COMPARECEU` | Obrigatória se efetivada |
| FLX-16 | Consulta | Consulta | Gerencia | Bloqueio impede reserva | Nenhum ou pendente | Conforme política |
| FLX-17 | Consulta | Consulta | Gerencia | Manutenção impede reserva | Nenhum ou pendente | Conforme política |
| FLX-18 | Produz eventos | Produz eventos | Produz/consulta | Mudança de estado auditada | Qualquer estado | Obrigatória na mudança |
| FLX-19 | Recebe | Recebe | Recebe | Evento/canal pendentes | Nenhum | Conforme política |
| FLX-20 | Sem permissão definida | Sem permissão definida | Consulta | Dados e fórmula pendentes | Nenhum | Conforme política |
| FLX-21 | Recebe erro | Recebe erro | Recebe erro | Erro seguro | Nenhum | Conforme política |
| FLX-22 | Usa documentação | Usa documentação | Usa/documenta | Documentar estados e autorização | Nenhum | Versionamento pendente |

## 11. Matriz de Permissões

| Operação | Solicitante | Responsável | Administrador | Observação |
|---|---|---|---|---|
| Consultar recursos | PERMITIDO | CONDICIONAL | PERMITIDO | Responsável conforme fluxo; detalhes de visibilidade pendentes. |
| Pesquisar disponibilidade | PERMITIDO | CONDICIONAL | PERMITIDO | Deve considerar reservas, agenda, manutenção e bloqueios. |
| Criar reserva | PERMITIDO | NEGADO | NEGADO | Solicitante cria a própria solicitação; exceções não definidas. |
| Alterar reserva própria | CONDICIONAL | NEGADO | PENDENTE DE DECISÃO | Permitida ao Solicitante somente em estados/condições ainda parcialmente definidos. |
| Cancelar reserva própria | CONDICIONAL | NEGADO | PENDENTE DE DECISÃO | Não pode apagar reserva iniciada; estados de origem pendentes. |
| Aprovar recurso restrito | NEGADO | PERMITIDO | NEGADO | Somente Responsável autorizado. |
| Rejeitar solicitação especial | NEGADO | PERMITIDO | NEGADO | Responsável decide dentro de sua responsabilidade. |
| Validar professor | NEGADO | PERMITIDO | NEGADO | Validação da alocação docente. |
| Registrar retirada | NEGADO | PERMITIDO | NEGADO | Material/equipamento deve estar associado à reserva. |
| Registrar devolução | NEGADO | PERMITIDO | NEGADO | Exige retirada correspondente. |
| Gerenciar salas | NEGADO | NEGADO | PERMITIDO | Administrador. |
| Gerenciar professores | NEGADO | NEGADO | PERMITIDO | Professor pode ser recurso; gestão é administrativa. |
| Gerenciar materiais | NEGADO | NEGADO | PERMITIDO | Inclui materiais e equipamentos conforme escopo. |
| Gerenciar usuários | NEGADO | NEGADO | PERMITIDO | Somente perfis oficiais. |
| Gerenciar bloqueios | NEGADO | NEGADO | PERMITIDO | Efeito sobre reservas existentes pendente. |
| Gerenciar manutenção | NEGADO | NEGADO | PERMITIDO | Recursos em manutenção não podem ser reservados. |
| Consultar auditoria | CONDICIONAL | CONDICIONAL | PERMITIDO | PRD cita histórico autorizado; visibilidade específica pendente. |
| Consultar relatórios | NEGADO | PENDENTE DE DECISÃO | PERMITIDO | Persona Administrador possui permissão; demais perfis não estão definidos. |

## 12. Matriz de Estados

| Estado atual | Ação | Próximo estado | Persona autorizada | Condições | Auditoria | Definição |
|---|---|---|---|---|---|---|
| `SOLICITADA` | Aprovar recurso restrito | `APROVADA` | Responsável | Solicitação autorizada, disponibilidade revalidada, sem conflito | Obrigatória | Confirmada no fluxo principal, detalhes pendentes |
| `SOLICITADA` | Rejeitar solicitação | `REJEITADA` | Responsável | Solicitação sob responsabilidade | Obrigatória | Estado e operação oficiais; motivo pendente |
| `SOLICITADA` | Cancelar | `CANCELADA` | PENDENTE DE DECISÃO | Condição e ator não completos | Obrigatória se efetivada | PENDENTE DE DECISÃO |
| `SOLICITADA` | Avançar fluxo | `APROVADA` | PENDENTE DE DECISÃO | Estado inicial não restrito não definido | Obrigatória | PENDENTE DE DECISÃO |
| `APROVADA` | Iniciar uso | `EM_USO` | PENDENTE DE DECISÃO | Momento e perfil não definidos | Obrigatória | PENDENTE DE DECISÃO |
| `APROVADA` | Cancelar | `CANCELADA` | PENDENTE DE DECISÃO | Se cancelamento antes do início for aprovado | Obrigatória | PENDENTE DE DECISÃO |
| `APROVADA` | Não comparecimento | `NAO_COMPARECEU` | PENDENTE DE DECISÃO | Origem, momento e perfil não definidos | Obrigatória | PENDENTE DE DECISÃO |
| `EM_USO` | Concluir | `CONCLUIDA` | PENDENTE DE DECISÃO | Perfil, devolução e validações não definidos | Obrigatória | PENDENTE DE DECISÃO |
| `EM_USO` | Apagar | Nenhum | Todos | Proibido pela regra de reserva iniciada | Tentativa conforme política | Confirmada como proibida |
| `CONCLUIDA` | Qualquer transição | PENDENTE DE DECISÃO | PENDENTE DE DECISÃO | Não especificada | PENDENTE | PENDENTE DE DECISÃO |
| `REJEITADA` | Qualquer transição | PENDENTE DE DECISÃO | PENDENTE DE DECISÃO | Não especificada | PENDENTE | PENDENTE DE DECISÃO |
| `CANCELADA` | Qualquer transição | PENDENTE DE DECISÃO | PENDENTE DE DECISÃO | Não especificada | PENDENTE | PENDENTE DE DECISÃO |
| `NAO_COMPARECEU` | Qualquer transição | PENDENTE DE DECISÃO | PENDENTE DE DECISÃO | Não especificada | PENDENTE | PENDENTE DE DECISÃO |

## 13. Matriz de Riscos

| Risco | Personas afetadas | Fluxo | Impacto | Controle esperado | Evidência |
|---|---|---|---|---|---|
| Dupla reserva | Solicitante; Administrador | FLX-05/06 | Reserva inconsistente | Validação concorrente com uma única aceitação | Teste concorrente e Testcontainers |
| Sobreposição na agenda do professor | Solicitante; Responsável | FLX-04/05/07 | Docente alocado em conflito | Verificar agenda na pesquisa, criação e aprovação | Testes parametrizados, API e integração |
| Reserva de recurso em manutenção | Solicitante; Responsável | FLX-04/05/17 | Uso de recurso indisponível | Considerar manutenção na pesquisa e reservar | E2E e API negativa |
| Aprovação por perfil indevido | Solicitante; Responsável; Administrador | FLX-01/07/14 | Contorno de governança | Autorização positiva/negativa no back-end | Testes de segurança e API |
| IDOR/acesso à reserva de outro usuário | Solicitante; demais perfis | FLX-01/08/09 | Exposição/alteração indevida | Verificar proprietário e escopo da autorização | API black-box e E2E |
| Exclusão de reserva iniciada | Todas | FLX-09/10 | Perda de rastreabilidade | Impedir apagamento após `EM_USO` | Teste de autorização e integração |
| Alteração sem auditoria | Todas | FLX-08/18 | Histórico incompleto | Auditar mudanças de estado e política operacional | Testcontainers e consulta de histórico |
| Retirada sem registro | Responsável; Solicitante | FLX-11 | Perda de controle material | Exigir registro associado à reserva | Integração e E2E |
| Devolução não registrada | Responsável; Administrador | FLX-12/13 | Recurso indisponível ou conclusão inconsistente | Vincular devolução a retirada | Integração e teste negativo |
| Falha na notificação | Todas | FLX-19 | Comunicação incompleta | Tratar falha sem corromper operação principal | WireMock |
| Relatório inconsistente | Administrador | FLX-20 | Controle operacional incorreto | Validar dados e fórmula aprovada | API, integração e dados controlados |
| Mensagem expõe detalhes internos | Todas | FLX-21 | Risco de segurança | Erros sem stack trace, credenciais, SQL ou caminhos | API, E2E, SonarCloud |
| Manutenção criada sobre reserva existente | Solicitante; Responsável; Administrador | FLX-17 | Conflito de disponibilidade | Política de reservas existentes pendente | Teste após decisão |
| Perfis ou usuários mal associados | Todas | FLX-03 | Acesso indevido | Restringir aos três perfis oficiais | Testes positivos/negativos |
| Professor usuário confundido com recurso | Solicitante; Responsável | FLX-02/04/07 | Autorização ou agenda incorreta | Separar conta/perfil de agenda/recurso | Revisão arquitetural e testes |

## 14. Estratégia de Validação dos Fluxos

| Técnica | Fluxos e uso |
|---|---|
| JUnit 5 | RN-01, estados, autorização contextual, conflito e validações isoladas. |
| Testes parametrizados | FLX-04/05/06/08/21 para horários, recursos, perfis, estados e entradas inválidas. |
| Testes de integração | FLX-02/03/05/07/08/11/12/13/16/17/18/20 para persistência, transações, disponibilidade e auditoria. |
| Testcontainers | Banco realista para reservas, estados, auditoria, manutenção, movimentação e concorrência. |
| API em caixa-preta | FLX-01/04/05/06/07/08/09/14/19/20/21/22 para contratos, autorização, códigos e erros. |
| WireMock | FLX-19 para notificação/API externa, sucesso, erro, timeout e resposta inválida. |
| End-to-end | Jornadas completas do Solicitante, Responsável e Administrador e cenários A-I. |
| Teste automatizado de concorrência | FLX-06 e cenário E, comprovando somente uma reserva aceita. |
| Teste de segurança | FLX-01, FLX-07, FLX-08, FLX-09 e cenário I, com casos positivos e negativos. |
| JMeter | FLX-04, FLX-05 e FLX-20 após aprovação de carga, taxa de erro, duração e percentis. Nenhum resultado é declarado. |
| JaCoCo | Gate oficial de mínimo de 80% de linhas e 70% de branches; cobertura não substitui testes de risco. |
| SonarCloud | Análise estática e verificação de zero vulnerabilidades críticas conhecidas. Nenhum resultado é declarado. |
| GitHub Actions | Execução em pull requests; critérios de bloqueio adicionais permanecem pendentes. |
| TDD/BDD | Evidência em pelo menos uma funcionalidade nova, preferencialmente reserva ou concorrência; ainda não executada. |

### Critérios de validação dos fluxos críticos

- Concorrência deve demonstrar uma reserva aceita e outra recusada sem inconsistência.
- Autorização deve demonstrar operações permitidas e negadas para cada perfil.
- Persistência crítica não pode depender apenas de mocks.
- Cada mudança de estado efetivada deve ter evidência de auditoria.
- Erros devem ser observáveis, compreensíveis e seguros.
- Metas de cobertura e qualidade são metas oficiais, não resultados já atingidos.

## 15. Candidatos para Avaliação da Equipe

### Candidato 1: Estado inicial de reserva não restrita

- **Descrição:** definir se reserva não restrita começa em `SOLICITADA` ou em outro ponto do fluxo oficial.
- **Origem:** FLX-05 e matriz de estados.
- **Benefício:** torna criação, ocupação e concorrência determinísticas.
- **Risco:** escolher sem aprovação altera a máquina de estados.
- **Decisão necessária:** aprovar estado inicial e ocupação de recursos.
- **Status:** NÃO APROVADO.

### Candidato 2: Política de notificação

- **Descrição:** escolher simulação ou API externa e definir evento, canal, destinatário, conteúdo e falha.
- **Origem:** RF-20/FLX-19.
- **Benefício:** torna comunicação verificável.
- **Risco:** cria escopo de integração sem decisão.
- **Decisão necessária:** aprovar alternativa e contrato.
- **Status:** NÃO APROVADO.

### Candidato 3: Política de transições

- **Descrição:** definir atores, condições e próximos estados para cancelamento, não comparecimento, início e conclusão.
- **Origem:** FLX-10, FLX-13, FLX-15 e matriz de estados.
- **Benefício:** remove ambiguidades de autorização e teste.
- **Risco:** inventar estados/transições.
- **Decisão necessária:** aprovar apenas transições necessárias.
- **Status:** NÃO APROVADO.

### Candidato 4: Modelo professor-usuário/professor-recurso

- **Descrição:** definir relação entre conta, perfil Solicitante e recurso professor/agendamento.
- **Origem:** seção 5 e revisão Architect.
- **Benefício:** evita conflitos de identidade e autorização.
- **Risco:** introduzir entidade ou regra não aprovada.
- **Decisão necessária:** aprovar relação e visibilidade de dados.
- **Status:** NÃO APROVADO.

### Candidato 5: Política de manutenção sobre reservas existentes

- **Descrição:** decidir se reserva existente é mantida, cancelada, rejeitada ou sinalizada quando surge manutenção.
- **Origem:** FLX-17.
- **Benefício:** evita inconsistência de disponibilidade.
- **Risco:** decisão tem efeito operacional amplo.
- **Decisão necessária:** aprovar comportamento para cada estado afetado.
- **Status:** NÃO APROVADO.

### Candidato 6: Fórmula e filtros de relatórios

- **Descrição:** definir cálculo de utilização, carga horária e conflitos evitados, além de filtros e agrupamento.
- **Origem:** FLX-20.
- **Benefício:** torna os relatórios objetivos e testáveis.
- **Risco:** inventar fórmula ou indicador.
- **Decisão necessária:** aprovar campos, período, fórmula, formato e perfis.
- **Status:** NÃO APROVADO.

### Candidato 7: Metas de desempenho e acessibilidade

- **Descrição:** definir carga, percentis, taxa de erro, duração, viewports, dispositivos e critérios de acessibilidade.
- **Origem:** RNF-14, RNF-16, FLX-21.
- **Benefício:** viabiliza aprovação objetiva.
- **Risco:** números e padrões não estão nas fontes.
- **Decisão necessária:** aprovar metas e cenários.
- **Status:** NÃO APROVADO.

### Candidato 8: Política de auditoria operacional

- **Descrição:** definir campos, retenção, visibilidade, tentativas recusadas e alteração de registros.
- **Origem:** FLX-18 e riscos.
- **Benefício:** consolida evidência de rastreabilidade.
- **Risco:** armazenar dados desnecessários ou criar obrigação não aprovada.
- **Decisão necessária:** aprovar política mínima e de minimização.
- **Status:** NÃO APROVADO.

## 16. Pendências e Lacunas

1. Qual estado uma reserva não restrita assume inicialmente e se `SOLICITADA` já ocupa os recursos.
2. De quais estados uma reserva pode ser cancelada e se cancelamento exige motivo.
3. De qual estado uma reserva pode ir para `NAO_COMPARECEU`.
4. Qual perfil registra `NAO_COMPARECEU` e em qual momento.
5. Quais estados permitem alteração.
6. Se alteração de recurso restrito exige nova aprovação.
7. Se alteração de professor após validação exige nova validação.
8. Quando e por qual perfil uma reserva passa para `EM_USO`.
9. Quem pode concluir uma reserva e se devolução pendente impede `CONCLUIDA`.
10. Quando recursos são liberados após cancelamento, rejeição, devolução e conclusão.
11. O que caracteriza recurso restrito e solicitação especial.
12. Qual é a responsabilidade exata do Responsável e sua visibilidade de solicitações.
13. Como se relacionam professor como usuário e professor como recurso.
14. Como bloqueio se diferencia de manutenção e quais efeitos possuem sobre reservas existentes.
15. Quais campos e validações são obrigatórios para cadastros e solicitações.
16. Quais são os campos, retenção, visibilidade e imutabilidade do histórico.
17. Qual alternativa de notificação será adotada, com evento, canal, destinatário, conteúdo e tratamento de falha.
18. Qual fórmula, filtro, período, formato e autorização se aplicam aos relatórios.
19. Quais metas de desempenho, carga, taxa de erro, duração, viewports e acessibilidade serão aprovadas.
20. Quais códigos HTTP, formato de erro, correlação e critérios adicionais de CI serão adotados.
21. Se usuário pode ter mais de um perfil, como desativação afeta reservas e se alteração de perfil é imediata.
22. Se término de uma reserva pode coincidir com início de outra.
23. Como alterações, aprovações, cancelamentos e concorrências simultâneas serão tratadas em todos os cenários além do caso mínimo.
24. Se Responsável pode consultar todas as reservas ou somente as sob sua responsabilidade.
25. Qual é a política para retirada/devolução duplicada, parcial, atrasada ou divergente.

## 17. Checklist Final

- [x] PASSOU: os três arquivos de personas foram analisados integralmente.
- [x] PASSOU: somente Solicitante, Responsável e Administrador foram utilizados.
- [x] PASSOU: nenhuma persona fictícia foi criada.
- [x] PASSOU: o contexto de cada persona foi enriquecido.
- [x] PASSOU: objetivos, necessidades, permissões e restrições foram detalhados.
- [x] PASSOU: a diferença entre professor como usuário e professor como recurso foi explicada.
- [x] PASSOU: a jornada completa do Solicitante foi documentada.
- [x] PASSOU: a jornada completa do Responsável foi documentada.
- [x] PASSOU: a jornada completa do Administrador foi documentada.
- [x] PASSOU: autenticação e autorização foram cobertas.
- [x] PASSOU: pesquisa e disponibilidade foram cobertas.
- [x] PASSOU: criação, alteração e cancelamento foram cobertos.
- [x] PASSOU: a agenda do professor foi considerada.
- [x] PASSOU: a proteção contra dupla reserva foi coberta.
- [x] PASSOU: recursos restritos exigem aprovação do Responsável.
- [x] PASSOU: manutenção e bloqueio foram cobertos.
- [x] PASSOU: retirada e devolução foram cobertas.
- [x] PASSOU: auditoria de mudanças de estado foi coberta.
- [x] PASSOU: reservas iniciadas não podem ser apagadas.
- [x] PASSOU: notificações e falhas de integração foram cobertas sem declarar execução.
- [x] PASSOU: relatórios foram cobertos.
- [x] PASSOU: estados confirmados e pendentes foram separados.
- [x] PASSOU: fluxos principais, alternativos e de exceção foram documentados.
- [x] PASSOU: matrizes de participação, permissões, estados e riscos foram criadas.
- [x] PASSOU: cada fluxo possui critérios de sucesso.
- [x] PASSOU: cada fluxo crítico possui evidência ou teste sugerido.
- [x] PASSOU: nenhuma funcionalidade do Foot Fanatics foi incorporada.
- [x] PASSOU: nenhuma decisão de negócio foi inventada.
- [x] PASSOU: candidatos não aprovados foram separados.
- [x] PASSOU: pendências foram registradas.
- [x] PASSOU: o arquivo foi salvo em `docs/fluxos-personas.md`.

### Resultado da revisão multidisciplinar

- **Analyst:** PASSOU. Objetivos, necessidades, jornadas, cenários e lacunas foram derivados das fontes.
- **Product Manager:** PASSOU. Escopo foi limitado a Organização de Recursos, sem duplicidade operacional indevida ou importação de Foot Fanatics.
- **Architect:** PASSOU. Perfis, professor-usuário/recurso, concorrência, manutenção, estados e auditoria foram revisados; lacunas não foram resolvidas por inferência.
- **QA:** PASSOU COM PENDÊNCIAS. Fluxos e evidências são testáveis, mas metas, estados, notificações, relatórios e critérios de autorização dependem das decisões listadas.

## Resultado da Documentação

- **Arquivo:** `docs/fluxos-personas.md`.
- **Personas analisadas:** 3.
- **Fluxos documentados:** 22, de FLX-01 a FLX-22.
- **Cenários integrados:** 9, de A a I.
- **Riscos identificados:** 15.
- **Pendências:** 25.
- **Candidatos não aprovados:** 8.
- **Checklist:** todos os itens como `PASSOU`; a revisão QA registra pendências de decisão humana sem tratá-las como falha documental.
- **Confirmação:** nenhuma persona adicional foi criada e nenhuma regra não aprovada foi apresentada como oficial. Nenhum código-fonte, teste ou arquivo além deste documento foi criado ou alterado nesta tarefa.
