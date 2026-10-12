# profile-service

Serviço responsável pelo domínio de **Perfis e Profissionais** do Marketplace para Serviços de Beleza.

Gerencia as informações pessoais dos usuários, a apresentação pública dos profissionais e a habilitação dos perfis para contratação.

## Objetivo

Permitir que clientes e profissionais mantenham seus perfis e que visitantes e clientes consultem as informações públicas dos profissionais antes de contratar um serviço.

## Responsabilidades

- Permitir a consulta e a atualização do próprio perfil.
- Gerenciar a apresentação pública dos profissionais.
- Manter a categoria de atuação e os links profissionais.
- Verificar os requisitos para habilitar um perfil profissional para contratação.
- Disponibilizar somente as informações autorizadas para consulta pública.
- Integrar informações de serviços, avaliações e disponibilidade na consulta do perfil profissional.

## Escopo funcional

| Caso de uso | Funcionalidade | Escopo |
| --- | --- | --- |
| UC-PER-01 | Consultar perfil pessoal | MVP |
| UC-PER-02 | Atualizar perfil pessoal | MVP |
| UC-PER-03 | Criar perfil profissional | MVP |
| UC-PER-04 | Disponibilizar perfil para contratação | MVP |
| UC-PER-05 | Consultar perfil público de profissional | MVP |

Requisitos relacionados: **RF-PRO-01 — Perfil profissional**, **RF-PRO-07 — Redes sociais** e **RF-CLI-03 — Perfil profissional**.

## Atores

| Ator | Relação com o domínio |
| --- | --- |
| Visitante | Consulta perfis profissionais disponíveis publicamente. |
| Cliente | Consulta e atualiza o próprio perfil e visualiza perfis profissionais. |
| Profissional | Mantém o próprio perfil e solicita sua habilitação para contratação. |
| Administrador | Administra perfis profissionais conforme suas permissões. |

## Conceitos do domínio

| Conceito | Descrição |
| --- | --- |
| Perfil pessoal | Informações do usuário vinculadas à sua conta. |
| Perfil profissional | Apresentação do profissional na plataforma. |
| Categoria de atuação | Classificação da atividade profissional. |
| Links profissionais | Endereços externos utilizados para apresentar o trabalho do profissional. |
| Habilitação para contratação | Condição que permite ao profissional receber contratações conforme as regras da plataforma. |

## Regras de negócio

### Perfil pessoal

- O usuário deve estar autenticado para consultar ou atualizar o próprio perfil.
- O perfil deve estar vinculado à identidade da conta.
- Somente os campos permitidos podem ser alterados.
- As informações devem ser validadas no backend.
- Caso o perfil esteja incompleto, o sistema deve apresentar os dados disponíveis e indicar as pendências.

### Perfil profissional

- O profissional deve estar autenticado para criar ou atualizar seu perfil.
- Os dados obrigatórios de apresentação devem ser informados.
- A categoria de atuação deve ser válida.
- Links profissionais podem ser informados quando desejado.
- A criação do perfil não implica sua habilitação automática para contratação.

### Habilitação para contratação

- **RB-02:** o profissional deve fornecer as informações mínimas necessárias antes de disponibilizar serviços para contratação.
- O perfil profissional deve existir.
- Os dados obrigatórios devem estar preenchidos.
- Deve existir pelo menos um serviço cadastrado.
- As demais condições de ativação definidas pela plataforma devem ser atendidas.
- Pendências devem ser apresentadas ao profissional.
- Os critérios exatos de verificação de identidade e ativação ainda dependem de definição do produto.

### Consulta pública

- Somente perfis disponíveis para consulta pública podem ser apresentados.
- Dados pessoais restritos não devem ser expostos.
- A consulta deve apresentar as informações públicas do profissional e sua categoria de atuação.
- Serviços, preços, durações, avaliações, disponibilidade e links profissionais devem ser apresentados conforme as integrações disponíveis.
- Informações pertencentes a outros domínios devem preservar suas respectivas fontes de referência.

## Limites do domínio

| Responsabilidade | Domínio responsável |
| --- | --- |
| Perfil pessoal, apresentação pública e habilitação profissional | Perfis e Profissionais |
| Contas, credenciais, autenticação e permissões | Identidade e Acesso |
| Categorias e ofertas de serviços, preços e duração | Catálogo de Serviços |
| Horários disponíveis e bloqueios | Agenda e Disponibilidade |
| Reservas e acompanhamento dos atendimentos | Agendamentos |
| Avaliações e reputação | Avaliações |
| Pesquisa, filtros e ordenação | Descoberta e Busca |
| Moderação e supervisão administrativa | Administração e Moderação |

O `profile-service` utiliza o identificador da conta fornecido pelo domínio de Identidade e Acesso. Senhas e credenciais não pertencem ao perfil.

Serviços, avaliações e disponibilidade podem compor a apresentação pública, mas suas regras e seus dados permanecem sob responsabilidade dos domínios correspondentes.

## Fluxos principais

### Consultar perfil pessoal

1. O usuário autenticado solicita o próprio perfil.
2. O sistema identifica a conta.
3. Recupera as informações correspondentes.
4. Apresenta os dados disponíveis e eventuais pendências.

### Atualizar perfil pessoal

1. O usuário solicita a edição do próprio perfil.
2. O sistema apresenta os dados atuais.
3. O usuário altera os campos permitidos.
4. O sistema valida e salva as alterações.
5. Confirma a atualização.

### Criar perfil profissional

1. O profissional autenticado acessa a configuração do perfil.
2. Informa os dados de apresentação.
3. Seleciona sua categoria de atuação.
4. Adiciona links profissionais, quando desejado.
5. O sistema valida e registra o perfil.
6. Informa as etapas restantes para habilitar a contratação.

### Habilitar perfil para contratação

1. O profissional solicita a ativação do perfil.
2. O sistema verifica os dados obrigatórios.
3. Verifica a existência de pelo menos um serviço cadastrado.
4. Verifica as demais condições definidas pela plataforma.
5. Habilita o perfil ou apresenta as pendências.

### Consultar perfil público

1. O visitante ou cliente acessa o perfil do profissional.
2. O sistema verifica se o perfil está disponível publicamente.
3. Recupera as informações públicas.
4. Consulta os dados relacionados de serviços, avaliações e disponibilidade.
5. Apresenta as informações autorizadas.

## Segurança e integridade

- Validar os dados recebidos no backend.
- Verificar a identidade e a autorização antes de alterar um perfil.
- Impedir alterações indevidas em perfis de outros usuários.
- Separar informações públicas e restritas.
- Restringir operações administrativas a usuários autorizados.
- Validar os formatos e protocolos permitidos nos links profissionais.
- Preservar a integridade da referência entre perfil e conta.
- Não confirmar alterações que não tenham sido persistidas.

## Fora do escopo do MVP

- Portfólio interno com galeria de fotos.
- Estruturas complexas de múltiplos estabelecimentos.
- Integrações sociais avançadas.
- Recomendações por inteligência artificial.
- Anúncios e destaques patrocinados.

Links para redes sociais profissionais fazem parte do escopo previsto e não representam uma integração social avançada.

## Arquitetura

Este README delimita o domínio do `profile-service`.

Os documentos de referência utilizam um **monólito modular orientado a domínios**. A implantação como microserviço independente deve ser documentada conforme a decisão arquitetural da equipe.

A implementação deve preservar a separação entre regras de domínio, casos de uso e integrações técnicas.

## Documentação técnica

Adicionar conforme a implementação:

- Tecnologias e versões utilizadas.
- Pré-requisitos e configuração local.
- Variáveis de ambiente.
- Configuração do banco de dados.
- Comandos de inicialização e execução dos testes.
- Endpoints e contratos da API.
- Regras de autenticação e autorização.
- Formato das respostas de erro.
- Contratos de integração com os demais domínios.

## Critérios de aceite

- [ ] Consultar o próprio perfil mediante autenticação.
- [ ] Apresentar informações disponíveis quando o perfil estiver incompleto.
- [ ] Atualizar somente os campos permitidos.
- [ ] Rejeitar informações inválidas.
- [ ] Impedir alterações não autorizadas em perfis de outros usuários.
- [ ] Criar perfil profissional com os dados obrigatórios.
- [ ] Validar a categoria de atuação.
- [ ] Permitir o cadastro de links profissionais válidos.
- [ ] Impedir habilitação sem os dados obrigatórios.
- [ ] Impedir habilitação sem pelo menos um serviço cadastrado.
- [ ] Apresentar as pendências que impedem a habilitação.
- [ ] Disponibilizar somente perfis autorizados para consulta pública.
- [ ] Preservar a privacidade dos dados restritos.
- [ ] Apresentar informações relacionadas conforme os contratos de integração.

## Decisões pendentes

- Campos obrigatórios dos perfis pessoal e profissional.
- Campos permitidos para edição pelo usuário.
- Dados que podem ser apresentados publicamente.
- Critérios de verificação de identidade do profissional.
- Condições completas de habilitação para contratação.
- Regras de visibilidade para perfis ainda não habilitados.
- Efeito da suspensão da conta sobre a visibilidade do perfil.
- Comportamento quando o profissional remove seu último serviço.
- Contratos de consulta a serviços, avaliações e disponibilidade.
- Tratamento de falhas nas integrações.
- Implantação como módulo ou microserviço independente.

## Referências

- Documento de Requisitos de Software — Marketplace para Serviços de Beleza.
- Especificação de Casos de Uso — Marketplace para Serviços de Beleza, versão 1.0.

> Este README descreve o escopo previsto. Os critérios de aceite não representam funcionalidades já implementadas ou testes já executados.