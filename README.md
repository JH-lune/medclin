Medclin — Sistema de Agendamento e Gestão de Consultas Médicas

Universidade Federal do Amazonas (UFAM)
Instituto de Ciências Exatas e Tecnologia (ICET)
Curso: Engenharia de Software
Disciplina: Engenharia de Requisitos
Ano: 2026

Integrantes

- João Henrique de Souza Barros
- Lúcia Vitória dos Santos Menezes
- Rhuan Felipe Neves Sena

Docente: Walter Jonas

---

# 1. Introdução

## 1.1. Descrição Geral do Software

O Medclin é um sistema web desenvolvido com a proposta de centralizar o agendamento e o controle administrativo de consultas em uma clínica médica.

A plataforma permite consultar horários disponíveis, realizar agendamentos, cancelamentos e reagendamentos, além de acompanhar os compromissos registrados no sistema.

O sistema contempla diferentes perfis de acesso, oferecendo aos pacientes o gerenciamento de suas consultas, aos recepcionistas o suporte nas operações de agendamento, aos médicos o gerenciamento de suas agendas e aos administradores o controle dos profissionais, relatórios e registros de auditoria.

O objetivo principal do Medclin é reduzir conflitos de horários, evitar retrabalho e facilitar o gerenciamento das consultas por meio de uma plataforma centralizada.

## 1.2. Descrição dos Usuários

O Medclin possui os seguintes perfis de usuários:

- **Paciente:** pode criar e atualizar seu cadastro, acessar o sistema, consultar médicos e horários disponíveis, agendar, visualizar, cancelar e reagendar suas próprias consultas.

- **Recepcionista:** pode acessar agendas, cadastrar e atualizar pacientes, realizar agendamentos e alterações em nome dos pacientes e registrar presenças.

- **Médico:** pode consultar sua própria agenda, definir horários de atendimento, configurar bloqueios e registrar o desfecho administrativo das consultas.

- **Administrador:** pode cadastrar, alterar, ativar e desativar médicos e especialidades, gerenciar agendas, consultar relatórios e acessar registros de auditoria.

- **Serviço de e-mail (externo):** recebe solicitações automáticas para o envio de confirmações, lembretes e notificações de alterações nas consultas.

# 2. Requisitos Gerais do Software

## 2.1. Requisitos Funcionais

Os requisitos funcionais descrevem as funcionalidades e os serviços que o sistema Medclin deverá oferecer aos seus usuários.

| ID   | Descrição                                                                                                          | Prioridade |
| ---- | ------------------------------------------------------------------------------------------------------------------ | ---------- |
| RF01 | Permitir a criação de contas de pacientes com nome, e-mail, telefone e senha, impedindo e-mails duplicados.        | Essencial  |
| RF02 | Autenticar usuários por e-mail e senha e liberar funcionalidades conforme o perfil autorizado.                     | Essencial  |
| RF03 | Permitir recuperação de senha por link temporário enviado ao e-mail cadastrado.                                    | Importante |
| RF04 | Listar médicos ativos e suas especialidades para seleção da consulta.                                              | Essencial  |
| RF05 | Exibir vagas futuras por médico/data, excluindo horários ocupados ou bloqueados.                                   | Essencial  |
| RF06 | Registrar consulta vinculada a paciente, médico, data e horário; gerar identificador e confirmação de agendamento. | Essencial  |
| RF07 | Exibir consultas do paciente e a agenda do profissional, com filtros por período e situação, conforme permissão.   | Essencial  |
| RF08 | Cancelar consulta elegível mediante confirmação e gravar motivo quando exigido.                                    | Essencial  |
| RF09 | Reagendar consulta elegível para outro slot disponível, preservando a consulta original se a operação falhar.      | Essencial  |
| RF10 | Permitir configurar dias, intervalos e duração dos slots de atendimento de um médico.                              | Essencial  |
| RF11 | Permitir bloquear intervalos da agenda e impedir novos agendamentos nesses períodos.                               | Importante |
| RF12 | Cadastrar, alterar, ativar e desativar profissionais e especialidades.                                             | Essencial  |
| RF13 | Registrar presença de paciente em consulta agendada.                                                               | Importante |
| RF14 | Permitir ao médico concluir a consulta como REALIZADA ou à recepção registrar NÃO_COMPARECEU nos casos aplicáveis. | Essencial  |
| RF15 | Registrar e solicitar envio de e-mail de confirmação, cancelamento ou reagendamento, sem expor dados clínicos.     | Importante |
| RF16 | Gerar lembrete de consultas futuras, preferencialmente 24 horas antes do horário.                                  | Desejável  |
| RF17 | Emitir resumo administrativo de consultas por período, profissional e situação, sem conteúdo clínico.              | Importante |
| RF18 | Permitir consultar registros de auditoria de operações relevantes, conforme autorização.                           | Importante |
| RF19 | Encerrar a sessão autenticada e invalidar o acesso da sessão encerrada.                                            | Essencial  |
| RF20 | Permitir atualizar dados de contato do paciente, respeitando titularidade e permissões.                            | Importante |

## 2.2. Requisitos Não Funcionais

Os requisitos não funcionais estabelecem critérios de qualidade, desempenho, segurança e restrições que o sistema Medclin deverá atender.

| ID    | Categoria             | Especificação                                                                                                              |
| ----- | --------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| RNF01 | Desempenho            | Em 95% das tentativas de autenticação, responder em até 2 segundos com até 100 sessões concorrentes.                       |
| RNF02 | Desempenho            | Em 95% das consultas de agenda, concluir a resposta em até 3 segundos, nas mesmas condições do RNF01.                      |
| RNF03 | Disponibilidade       | Meta de disponibilidade mensal de 99,5%, excluídas janelas de manutenção anunciadas.                                       |
| RNF04 | Segurança             | Proteger o tráfego do sistema com TLS 1.2 ou superior.                                                                     |
| RNF05 | Segurança             | Armazenar apenas derivação segura e salgada de senhas, nunca mantendo senhas em texto legível.                             |
| RNF06 | Controle de acesso    | Validar no servidor as permissões por papel e titularidade em todas as operações sensíveis.                                |
| RNF07 | Privacidade           | Tratar dados pessoais conforme finalidade, minimização, controle de acesso e política de retenção, considerando a LGPD.    |
| RNF08 | Usabilidade           | Oferecer interface responsiva, utilizável desde 360 px de largura, nos navegadores principais.                             |
| RNF09 | Acessibilidade        | Atender como meta aos critérios aplicáveis de nível AA da WCAG 2.1 nos fluxos essenciais, incluindo navegação por teclado. |
| RNF10 | Backup e recuperação  | Executar backup diário protegido e testar restauração, com metas iniciais de RPO ≤ 24 horas e RTO ≤ 4 horas.               |
| RNF11 | Consistência de dados | Impedir reservas simultâneas de um mesmo horário por meio de transação atômica e restrição de integridade.                 |
| RNF12 | Localização           | Exibir datas em pt-BR e horários na zona America/Manaus, armazenando os instantes de forma inequívoca.                     |

## 2.3. Regras de Negócio

As regras de negócio definem as condições e restrições que orientam o funcionamento do Medclin, estabelecendo critérios para agendamentos, cancelamentos, disponibilidade e gerenciamento das consultas.

| ID   | Regra de Negócio                                                                                                                |
| ---- | ------------------------------------------------------------------------------------------------------------------------------- |
| RN04 | Não pode haver duas consultas ativas no mesmo horário do mesmo médico nem consultas simultâneas para o mesmo paciente.          |
| RN05 | A duração sugerida do slot é de 30 minutos, passível de configuração por profissional.                                          |
| RN06 | Pacientes podem reservar consultas dentro de uma janela móvel proposta de 60 dias.                                              |
| RN07 | Paciente pode cancelar ou remarcar até 2 horas antes do início; recepção pode cancelar até o início, registrando justificativa. |
| RN08 | Remarcação é atômica: ao ocorrer indisponibilidade no novo horário, a reserva anterior permanece inalterada.                    |
| RN09 | Consultas CANCELADAS, REALIZADAS ou NÃO_COMPARECEU não podem ser reagendadas; nova consulta é um novo registro.                 |
| RN10 | Presença pode ser marcada a partir de 30 minutos antes do início; apenas profissional vinculado pode registrar REALIZADA.       |
| RN11 | NÃO_COMPARECEU só é permitido após terminar o horário previsto, por recepcionista autorizado.                                   |
| RN12 | Médico altera a própria disponibilidade; administrador pode gerir disponibilidades de todos os médicos.                         |
| RN13 | E-mails administrativos informam apenas profissional, data, hora e local, sem resultados ou dados clínicos.                     |
| RN14 | Operações de agendar, cancelar, remarcar, mudar situação e gerir agenda geram trilha de auditoria.                              |
| RN15 | Consultas canceladas não são excluídas do histórico; médicos desativados não recebem novos agendamentos.                        |

Política de estado das consultas: uma consulta inicia como AGENDADA e poderá passar para CANCELADA antes do início, REALIZADA após confirmação de presença e atendimento ou NÃO_COMPARECEU após a janela de atendimento. O simples registro de presença não equivale à finalização da consulta.

Observação: as regras de negócio são propostas iniciais e deverão ser validadas com a clínica.

### 3.1. Diagramas de Casos de Uso

**Figura 1 – Acesso e agendamento**

![Diagrama de casos de uso: acesso e agendamento](docs/diagramas/caso-uso-01-acesso-agendamento.png)

**Figura 2 – Operação e gestão**

![Diagrama de casos de uso: operação e gestão](docs/diagramas/caso-uso-02-operacao-gestao.png)

**Figura 3 – Conta e comunicação**

![Diagrama de casos de uso: conta e comunicação](docs/diagramas/caso-uso-03-conta-comunicacao.png)

### 3.2. Diagramas de Sequência

**Figura 4 – Agendamento de consulta (UC04)**

![Diagrama de sequência: agendamento](docs/diagramas/sequencia-01-agendamento.png)

**Figura 5 – Remarcação de consulta (UC05)**

![Diagrama de sequência: remarcação](docs/diagramas/sequencia-02-remarcacao.png)

**Figura 6 – Registro de desfecho (UC09)**

![Diagrama de sequência: registro de desfecho](docs/diagramas/sequencia-03-registro-desfecho.png)

### 3.3. Diagramas de Atividades

**Figura 7 – Agendar consulta**

![Diagrama de atividades: agendar consulta](docs/diagramas/atividade-01-agendar-consulta.png)

**Figura 8 – Remarcar consulta**

![Diagrama de atividades: remarcar consulta](docs/diagramas/atividade-02-remarcar-consulta.png)
