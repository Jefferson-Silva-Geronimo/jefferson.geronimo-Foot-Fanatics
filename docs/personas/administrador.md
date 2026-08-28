# Persona: Administrador

## Visão Geral
Gerencia salas, professores, materiais, usuários, bloqueios e períodos de manutenção.

## Objetivo Principal
Manter os recursos, usuários, bloqueios e períodos de manutenção organizados para permitir uma alocação sem conflitos de horário.

## Objetivos Específicos
- Manter salas, professores e materiais disponíveis para consulta e alocação.
- Manter os usuários associados aos perfis oficiais de acesso.
- Registrar bloqueios e períodos de manutenção para impedir reservas indevidas.
- Acompanhar a utilização dos recursos, a carga horária alocada e os conflitos evitados.
- Consultar o histórico auditável para apoiar rastreabilidade, auditoria e controle operacional.

## Casos de Uso

### Gerenciar recursos

1. Autentica-se no sistema como Administrador.
2. Cadastra ou consulta salas, professores e materiais.
3. Mantém os recursos disponíveis para pesquisa e alocação.

### Gerenciar usuários e perfis

1. Consulta os usuários do sistema.
2. Gerencia os usuários e seus perfis oficiais: Solicitante, Responsável e Administrador.
3. Mantém as informações necessárias para autenticação e autorização por perfil.

### Registrar bloqueio ou manutenção

1. Seleciona o recurso que precisa ficar indisponível.
2. Gerencia o bloqueio ou o período de manutenção correspondente.
3. O sistema considera o recurso indisponível para reservas no período registrado.
4. O sistema impede reservas em recurso que esteja em manutenção.

### Consultar relatórios operacionais

1. Consulta os dados de utilização dos recursos.
2. Consulta a carga horária alocada.
3. Consulta os conflitos evitados.
4. Usa os resultados para o controle operacional, sem permitir alocações com conflito.

### Consultar histórico auditável

1. Localiza o histórico de uma reserva ou operação registrada.
2. Consulta as mudanças de estado e os registros auditáveis disponíveis.
3. Usa o histórico para rastreabilidade e auditoria.

## Jornada da Persona

1. **Acesso:** autentica-se e recebe as permissões do perfil Administrador.
2. **Preparação:** cadastra e consulta salas, professores e materiais.
3. **Controle de acesso:** gerencia usuários e os perfis oficiais de autorização.
4. **Disponibilidade:** registra bloqueios e períodos de manutenção para proteger os recursos indisponíveis.
5. **Controle operacional:** consulta relatórios de utilização, carga horária alocada e conflitos evitados.
6. **Auditoria:** consulta o histórico auditável para acompanhar mudanças e apoiar a rastreabilidade.
7. **Respeito às responsabilidades:** não substitui a aprovação de solicitações especiais atribuída ao Responsável e não permite conflitos ou reservas em manutenção.

## Contexto de Atuação

O Administrador atua na preparação e na manutenção do ambiente operacional. Ele cadastra e consulta salas, professores, materiais e equipamentos, gerencia usuários e perfis oficiais, registra bloqueios e períodos de manutenção e consulta informações de controle. Sua atuação sustenta as pesquisas e reservas do Solicitante e fornece o contexto necessário para as decisões do Responsável.

O Administrador interage com todos os recursos gerenciados, mas não substitui a decisão do Responsável sobre recursos restritos. Seu privilégio administrativo não autoriza ignorar conflitos, indisponibilidade, auditoria ou a proibição de apagar reservas iniciadas.

## Necessidades de Informação

- Cadastros de salas, professores, materiais e equipamentos.
- Usuários e perfis `Solicitante`, `Responsável` e `Administrador`.
- Bloqueios e períodos de manutenção por recurso.
- Reservas potencialmente afetadas por indisponibilidade.
- Utilização por recurso, carga horária alocada e conflitos evitados.
- Estados das reservas e histórico auditável das operações.
- Efeitos das alterações administrativas sobre pesquisa e disponibilidade.

## Decisões do Perfil

- Decide cadastrar, consultar e atualizar recursos dentro do escopo.
- Decide gerenciar usuários e associar somente perfis oficiais.
- Decide registrar e manter bloqueios e períodos de manutenção.
- Decide consultar relatórios e histórico para controle operacional.
- Não decide aprovação de recurso restrito, fórmula de conflitos evitados, transições não especificadas ou política de reservas existentes afetadas por manutenção.

## Eventos que Iniciam a Atuação

- Necessidade de cadastrar ou atualizar sala, professor, material ou equipamento.
- Necessidade de criar ou atualizar usuário e perfil oficial.
- Necessidade de tornar um recurso indisponível por bloqueio ou manutenção.
- Necessidade de verificar impacto da indisponibilidade sobre a pesquisa e as reservas.
- Necessidade de consultar utilização, carga horária, conflitos evitados ou histórico.

## Resultados e Indicadores de Conclusão

- Recurso válido é cadastrado e pode ser consultado.
- Perfil é associado somente a um dos três perfis oficiais.
- Bloqueio e manutenção aparecem como indisponibilidade no período aplicável.
- Pesquisa e reserva não tratam recurso em manutenção ou bloqueado como disponível.
- Relatórios apresentam utilização, carga horária e conflitos evitados conforme definição aprovada.
- Alterações e mudanças de estado preservam rastreabilidade.

## Erros e Impedimentos Característicos

- Acesso negado a operação administrativa.
- Dados cadastrais inválidos ou recurso inexistente.
- Tentativa de criar perfil adicional.
- Bloqueio ou manutenção com período inválido.
- Manutenção ou bloqueio sobre reserva existente sem política aprovada.
- Tentativa de permitir conflito ou reserva em indisponibilidade.
- Tentativa de apagar reserva iniciada ou registro de auditoria.
- Tentativa de aprovar recurso restrito no lugar do Responsável.
- Relatório sem dados, filtro inválido ou fórmula ainda não definida.
- Falha de notificação ou integração externa.

## Auditoria e Notificações

Alterações de recursos, usuários, perfis, bloqueios e manutenção devem seguir a política de auditoria aprovada. Toda mudança de estado de reserva deve gerar auditoria, e registros necessários ao histórico não podem ser apagados pelos perfis operacionais. Notificações sobre alterações administrativas, indisponibilidade ou falhas não possuem evento, canal, destinatário ou conteúdo definidos.

## Riscos Operacionais

- Perfil associado incorretamente e autorização indevida.
- Cadastro ou estado de recurso desatualizado influenciando a disponibilidade.
- Manutenção ou bloqueio ignorado pela pesquisa ou pela reserva.
- Alteração administrativa sem auditoria.
- Uso do privilégio administrativo para contornar aprovação do Responsável.
- Perda de histórico por exclusão de reserva iniciada ou registro auditável.
- Relatório inconsistente por fórmula ou dados não definidos.

## Peculiaridades do Perfil

- É o perfil responsável por preparar o contexto que os demais utilizam, mas não é o aprovador de recursos restritos.
- Administra os três perfis oficiais; não pode criar personas ou perfis adicionais.
- Professor pode ser mantido como cadastro de recurso alocável mesmo quando a relação com um usuário autenticado ainda não estiver definida.
- Bloqueio e manutenção afetam a disponibilidade, mas a diferença operacional entre os dois conceitos ainda precisa de decisão.
- Deve preservar registros e rastreabilidade mesmo quando uma alteração administrativa afeta o fluxo de reservas.

## Responsabilidades
- Gerenciar salas.
- Gerenciar professores.
- Gerenciar materiais.
- Gerenciar usuários.
- Gerenciar bloqueios.
- Gerenciar períodos de manutenção.

## Funcionalidades Utilizadas
- Autenticação e autorização
- Gestão de salas
- Gestão de professores
- Gestão de materiais
- Gestão de usuários
- Gestão de bloqueios
- Gestão de manutenção
- Relatórios
- Histórico auditável

## Permissões
- Gerenciar salas.
- Gerenciar professores.
- Gerenciar materiais.
- Gerenciar usuários.
- Gerenciar bloqueios.
- Gerenciar períodos de manutenção.
- Consultar relatórios e histórico auditável para controle operacional, rastreabilidade e auditoria.

## Restrições
- Não pode permitir alocação que gere conflito de horário.
- Não pode permitir reserva de recursos em manutenção.
- Não pode apagar reservas iniciadas.
- Não pode substituir a aprovação de solicitações especiais atribuída aos responsáveis.

## Regras de Negócio Relacionadas
- Não pode gerar dupla reserva.
- Não pode reservar recursos em manutenção.
- Recursos restritos exigem aprovação.
- Toda alteração gera auditoria.
- Reservas iniciadas não podem ser apagadas.
- Apenas responsáveis aprovam recursos restritos.

## Critérios de Sucesso
- Salas, professores, materiais, usuários, bloqueios e períodos de manutenção estão gerenciados corretamente.
- A alocação ocorre sem conflitos de horário e sem uso de recursos em manutenção.
- Relatórios e histórico auditável permitem rastreabilidade, auditoria e controle operacional.
