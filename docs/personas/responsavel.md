# Persona: Responsável

## Visão Geral
Aprova solicitações especiais, valida a alocação de docentes e acompanha retiradas e devoluções de material.

## Objetivo Principal
Garantir a aprovação de solicitações especiais, a validação da alocação de docentes e o acompanhamento dos materiais retirados e devolvidos.

## Objetivos Específicos
- Avaliar solicitações especiais de recursos restritos.
- Validar se a alocação de docentes respeita a agenda do professor.
- Acompanhar a retirada de materiais e equipamentos associados às reservas.
- Acompanhar a devolução dos materiais e equipamentos retirados.
- Manter as decisões e movimentações rastreáveis por meio do histórico auditável.

## Casos de Uso

### Aprovar uma solicitação especial

1. Autentica-se no sistema como Responsável.
2. Consulta a solicitação especial de um recurso restrito.
3. Verifica as informações disponíveis para a decisão.
4. Aprova a solicitação quando ela atende às regras aplicáveis.
5. O sistema registra a mudança de estado em auditoria.

### Rejeitar uma solicitação especial

1. Consulta uma solicitação especial pendente.
2. Avalia a solicitação dentro de sua responsabilidade.
3. Rejeita a solicitação quando ela não atende às regras aplicáveis.
4. O sistema registra o estado `REJEITADA` e a mudança em auditoria.

### Validar a alocação de docentes

1. Consulta a alocação de um docente.
2. Verifica a agenda do professor no período da reserva.
3. Confirma a alocação quando não existe sobreposição.
4. O sistema não considera válida uma alocação que conflite com a agenda do professor.

### Registrar retirada de material

1. Localiza a reserva e o material ou equipamento associado.
2. Registra a retirada.
3. Acompanha a retirada registrada no sistema.

### Registrar devolução de material

1. Localiza a retirada registrada.
2. Registra a devolução do material ou equipamento.
3. Acompanha a devolução registrada no sistema.

## Jornada da Persona

1. **Acesso:** autentica-se e recebe as permissões do perfil Responsável.
2. **Análise:** consulta solicitações especiais e alocações de docentes sob sua responsabilidade.
3. **Decisão:** aprova ou rejeita solicitações especiais conforme as regras aplicáveis.
4. **Validação:** verifica a agenda do professor e registra o resultado da validação da alocação.
5. **Movimentação:** acompanha e registra a retirada de materiais ou equipamentos.
6. **Encerramento:** acompanha e registra a devolução correspondente.
7. **Rastreabilidade:** as mudanças de estado e registros decorrentes ficam auditáveis.

## Contexto de Atuação

O Responsável entra no fluxo quando existe uma solicitação especial de recurso restrito, uma alocação de docente a validar ou uma movimentação de material a acompanhar. Sua atuação depende de informações atuais da solicitação, do recurso, do período, da disponibilidade, da agenda do professor, da reserva e dos registros de retirada e devolução.

O Responsável interage com o Solicitante por meio da solicitação e com os recursos mantidos pelo Administrador. Ele exerce uma decisão específica dentro de sua responsabilidade, sem assumir a gestão de salas, professores, materiais, usuários, bloqueios ou manutenção.

## Necessidades de Informação

- Solicitação especial pendente e recurso restrito relacionado.
- Solicitante associado à solicitação.
- Período e disponibilidade atual no momento da decisão.
- Agenda do professor e possíveis sobreposições.
- Estado atual da reserva e transições aplicáveis.
- Reserva e material ou equipamento associado.
- Registro de retirada necessário para registrar a devolução.
- Histórico auditável das decisões e movimentações acessíveis ao perfil.

## Decisões do Perfil

- Aprova ou rejeita uma solicitação especial quando estiver autorizado para ela.
- Valida a alocação do docente quando não existir conflito na agenda do professor.
- Decide registrar uma retirada ou devolução quando as respectivas associações estiverem presentes.
- Não decide critérios ainda não definidos para recurso restrito, transições não especificadas, manutenção ou gestão administrativa.

## Eventos que Iniciam a Atuação

- Existência de solicitação especial pendente.
- Necessidade de validar uma alocação de docente.
- Existência de material ou equipamento associado a uma reserva para retirada.
- Existência de retirada registrada para devolução.

## Resultados e Indicadores de Conclusão

- A disponibilidade é revalidada antes da aprovação.
- Solicitação sem conflito pode passar a `APROVADA`.
- Solicitação que não atende às regras pode passar a `REJEITADA`, quando a operação estiver autorizada.
- Alocação docente sem sobreposição é registrada como validada.
- Retirada e devolução ficam associadas à reserva e podem ser acompanhadas.
- Decisões e mudanças de estado ficam auditáveis.

## Erros e Impedimentos Característicos

- Acesso negado por perfil ou por falta de responsabilidade sobre a solicitação.
- Solicitação inexistente, já decidida ou com estado não permitido.
- Conflito novo na agenda do professor.
- Disponibilidade alterada entre a criação e a decisão.
- Recurso em manutenção ou bloqueado.
- Tentativa de aprovar por Solicitante ou Administrador.
- Tentativa de registrar devolução sem retirada correspondente.
- Retirada ou devolução duplicada, caso essa regra seja aprovada.
- Tentativa de gerenciar cadastros ou alterar histórico.
- Falha de notificação ou integração externa.

## Auditoria e Notificações

Aprovação, rejeição, validação docente e mudanças de estado devem gerar auditoria. Retirada, devolução e tentativas recusadas devem seguir a política de auditoria a ser definida. O Responsável pode receber solicitações e resultados de decisões ou movimentações; os eventos, canal, destinatários e conteúdo das notificações permanecem pendentes.

## Riscos Operacionais

- Aprovar recurso restrito sem revalidar disponibilidade.
- Aprovar solicitação com conflito na agenda do professor.
- Permitir que outro perfil aprove ou que o Administrador contorne a aprovação.
- Registrar retirada sem associação à reserva ou devolução sem retirada.
- Produzir decisão sem auditoria ou notificação inconsistente.

## Peculiaridades do Perfil

- É o único perfil autorizado a aprovar recursos restritos.
- Sua aprovação não substitui a verificação de disponibilidade e conflito.
- A validação docente considera o professor como recurso alocável e sua agenda, não o perfil de usuário que eventualmente o represente.
- A devolução exige retirada correspondente; o fluxo não autoriza completar a movimentação sem esse vínculo.
- O alcance de "sua responsabilidade" não foi detalhado e deve ser definido pela equipe.

## Responsabilidades
- Aprovar solicitações especiais.
- Validar a alocação de docentes.
- Acompanhar retiradas de material.
- Acompanhar devoluções de material.

## Funcionalidades Utilizadas
- Autenticação e autorização
- Aprovação de solicitações especiais
- Validação de docentes
- Registro de retirada de materiais
- Registro de devolução de materiais

## Permissões
- Aprovar solicitações especiais.
- Validar a alocação de docentes.
- Acompanhar e registrar retiradas de materiais.
- Acompanhar e registrar devoluções de materiais.

## Restrições
- Não pode gerenciar salas, professores, materiais, usuários, bloqueios ou períodos de manutenção.
- Não pode criar, alterar ou cancelar reservas de outros solicitantes.
- Não pode aprovar recursos restritos fora de sua responsabilidade como responsável.

## Regras de Negócio Relacionadas
- Recursos restritos exigem aprovação.
- Apenas responsáveis aprovam recursos restritos.
- Toda alteração gera auditoria.

## Critérios de Sucesso
- As solicitações especiais são aprovadas quando atendem às regras aplicáveis.
- A alocação de docentes é validada.
- As retiradas e devoluções de materiais ficam registradas e acompanhadas.
