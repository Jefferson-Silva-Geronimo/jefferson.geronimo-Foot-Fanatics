# Persona: Solicitante

## Visão Geral
Professor ou coordenador que consulta a disponibilidade e cria, altera ou cancela suas reservas.

## Objetivo Principal
Organizar suas reservas de salas, professores e materiais sem conflitos de horário.

## Objetivos Específicos
- Encontrar salas, professores e materiais compatíveis com a necessidade da reserva.
- Confirmar a disponibilidade dos recursos no período desejado.
- Manter suas próprias reservas atualizadas ou cancelá-las quando necessário.
- Evitar conflitos de horário, inclusive na agenda do professor.

## Casos de Uso

### Consultar recursos e disponibilidade

1. Autentica-se no sistema como Solicitante.
2. Consulta salas, professores e materiais.
3. Pesquisa por tipo, capacidade, localização, competência e disponibilidade.
4. Verifica se o recurso está livre, bloqueado ou em manutenção no período desejado.

### Criar uma reserva

1. Seleciona os recursos e informa o início e o término da reserva.
2. O sistema verifica se o término é posterior ao início.
3. O sistema verifica conflitos na sala, no material e na agenda do professor.
4. O sistema impede a reserva se houver sobreposição, manutenção ou dupla reserva.
5. Se o recurso for restrito, a solicitação segue para aprovação do Responsável.

### Alterar uma reserva própria

1. Localiza uma reserva que criou.
2. Solicita a alteração dos dados permitidos da reserva.
3. O sistema verifica período, disponibilidade, manutenção e conflitos.
4. A alteração é aceita somente se respeitar as regras aplicáveis.
5. A mudança de estado, quando ocorrer, fica registrada em auditoria.

### Cancelar uma reserva própria

1. Localiza uma reserva que criou e que ainda não foi iniciada.
2. Solicita o cancelamento.
3. O sistema altera a reserva para `CANCELADA` e registra a mudança.

## Jornada da Persona

1. **Acesso:** autentica-se e recebe somente as permissões do perfil Solicitante.
2. **Busca:** consulta os recursos e pesquisa a disponibilidade usando os filtros disponíveis.
3. **Planejamento:** compara a disponibilidade da sala, do material e do professor no período desejado.
4. **Solicitação:** cria a reserva com início e término válidos; quando houver recurso restrito, a solicitação depende da aprovação aplicável.
5. **Acompanhamento:** consulta o resultado da solicitação e mantém suas reservas sob sua responsabilidade.
6. **Atualização:** altera ou cancela uma reserva própria conforme as regras de estado e de horário.
7. **Rastreabilidade:** as mudanças de estado ficam disponíveis no histórico auditável conforme as permissões do sistema.

## Contexto de Atuação

O Solicitante participa quando precisa encontrar e reservar uma sala, um professor, um material ou um equipamento. Sua atuação começa pela autenticação e pela consulta dos recursos preparados pelo Administrador. Quando seleciona um professor como recurso, a agenda desse professor também precisa ser considerada, independentemente de o professor possuir ou não uma conta de usuário.

O Solicitante interage principalmente com o sistema e depende do Administrador para que os cadastros, bloqueios e períodos de manutenção estejam atualizados. Quando a reserva envolve recurso restrito, sua solicitação depende da análise do Responsável.

## Necessidades de Informação

- Recursos cadastrados por tipo.
- Capacidade e localização das salas.
- Competência associada ao professor ou recurso pesquisado.
- Disponibilidade da sala, do material, do equipamento e do professor no período solicitado.
- Existência de reserva, bloqueio ou manutenção no intervalo.
- Estado e resultado das próprias reservas.
- Motivo observável de recusa, como período inválido, conflito, manutenção, bloqueio ou falta de autorização.
- Histórico auditável acessível ao seu perfil.

## Decisões do Perfil

- Escolhe os filtros de pesquisa e os recursos a solicitar.
- Informa o início e o término desejados.
- Decide criar, alterar ou cancelar uma reserva própria quando a operação estiver permitida.
- Não decide sobre aprovação de recurso restrito, validação da agenda docente ou gestão de recursos.

## Eventos que Iniciam a Atuação

- Necessidade de reservar recursos para uma atividade.
- Necessidade de confirmar a disponibilidade em determinado período.
- Necessidade de corrigir uma reserva própria ainda não iniciada, quando a alteração for permitida.
- Necessidade de cancelar uma reserva própria antes do início, quando o estado permitir.

## Resultados e Indicadores de Conclusão

- A pesquisa retorna recursos compatíveis e não apresenta como disponíveis os recursos em conflito, bloqueados ou em manutenção.
- A reserva é criada somente com término posterior ao início.
- Sala, material, equipamento e professor não possuem sobreposição para a reserva aceita.
- Em solicitações simultâneas, a reserva do Solicitante é aceita ou recusada de forma controlada.
- A própria reserva é alterada ou passa para `CANCELADA` somente quando autorizado.
- O motivo de uma recusa é apresentado sem detalhes internos.

## Erros e Impedimentos Característicos

- Tentativa de acessar uma operação de outro perfil.
- Término igual ou anterior ao início.
- Conflito de horário na sala, no material, no equipamento ou na agenda do professor.
- Recurso indisponível, bloqueado ou em manutenção.
- Outra solicitação simultânea aceita primeiro.
- Tentativa de acessar ou alterar reserva de outro Solicitante.
- Tentativa de alterar ou cancelar reserva iniciada.
- Tentativa de aprovar recurso restrito ou validar docente.
- Falha de notificação ou integração, conforme mecanismo que a equipe escolher.

## Auditoria e Notificações

Toda mudança de estado da reserva deve gerar auditoria. Criação, alteração, cancelamento, tentativa recusada e conteúdo mínimo do histórico dependem da política da equipe quando não houver mudança de estado. O Solicitante pode ser informado sobre criação, aprovação, rejeição, cancelamento e falha de comunicação, mas evento, canal, destinatário e conteúdo ainda não estão definidos.

## Riscos Operacionais

- Confundir uma consulta de disponibilidade com garantia de reserva, ignorando a validação final.
- Permitir acesso a reserva de outro usuário.
- Aceitar conflito na agenda do professor por verificar somente a sala.
- Aceitar reserva de recurso bloqueado ou em manutenção.
- Perder a trilha de alteração ou apresentar mensagem que exponha dados internos.

## Peculiaridades do Perfil

- Opera apenas o próprio conjunto de reservas.
- É o ponto de entrada da jornada de reserva, mas não controla cadastros nem aprovações.
- Pode ser professor ou coordenador como usuário autenticado; isso não elimina a necessidade de tratar o professor alocado como recurso de agenda.
- A consulta de disponibilidade é informativa até a confirmação da reserva, pois a concorrência pode alterar o resultado.

## Responsabilidades
- Consultar a disponibilidade de recursos.
- Criar suas reservas.
- Alterar suas reservas.
- Cancelar suas reservas.

## Funcionalidades Utilizadas
- Autenticação e autorização
- Consulta de recursos
- Pesquisa de disponibilidade
- Criação de reservas
- Alteração de reservas
- Cancelamento de reservas

## Permissões
- Consultar recursos e pesquisar sua disponibilidade.
- Criar reservas.
- Alterar suas reservas.
- Cancelar suas reservas.

## Restrições
- Não pode criar, alterar ou cancelar reservas de outros solicitantes.
- Não pode reservar recursos em manutenção.
- Não pode gerar dupla reserva.
- Não pode aprovar solicitações especiais.
- Não pode validar a alocação de docentes.
- Não pode gerenciar salas, professores, materiais, usuários, bloqueios ou períodos de manutenção.

## Regras de Negócio Relacionadas
- Não pode reservar recursos em manutenção.
- Não pode gerar dupla reserva.
- Recursos restritos exigem aprovação.
- Toda alteração gera auditoria.
- Reservas iniciadas não podem ser apagadas.
- Apenas responsáveis aprovam recursos restritos.

## Critérios de Sucesso
- A disponibilidade dos recursos é consultada corretamente.
- A reserva é criada sem conflito de horário ou é alterada ou cancelada conforme necessário.
- As alterações ficam rastreáveis e auditáveis.
