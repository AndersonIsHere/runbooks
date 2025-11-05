# Política de Concessão de Acesso Privilegiado

| **Documento:** | Política de Concessão de Acesso Privilegiado |
| :--- | :--- |
| **ID do Documento:** | `POL-SEG-002` |
| **Proprietário:** | Departamento de Segurança da Informação |
| **Aprovador:** | CISO (Chief Information Security Officer) |
| **Versão:** | `2.0` |
| **Status:** | Aprovado |
| **Data de Vigência:** | `2025-07-04` |
| **Próxima Revisão:** | `2026-01-04` |

---

## 1. Objetivo

Esta política estabelece as diretrizes e controles mandatórios para a solicitação, aprovação, concessão, gerenciamento, monitoramento e revogação de todo e qualquer acesso privilegiado aos sistemas, infraestrutura, aplicações e dados da `[Nome da Empresa]`.

O objetivo principal é mitigar o risco de comprometimento de dados, interrupção de serviços e atividades maliciosas, aplicando o **Princípio do Menor Privilégio (PoLP)** e garantindo a **rastreabilidade (accountability)** total das ações privilegiadas.

## 2. Escopo

Esta política se aplica a todos os sistemas, plataformas em nuvem (IaaS, PaaS, SaaS), bancos de dados, dispositivos de rede e aplicações. Ela é mandatória para todos os colaboradores, prestadores de serviço, consultores e sistemas automatizados (contas de serviço) que necessitem de acesso privilegiado.

## 3. Definições

* **Acesso Privilegiado:** Nível de acesso elevado (ex: `root`, `administrator`, `DBA`, `sysadmin`) que permite a um usuário ou serviço realizar ações de segurança, configuração ou gerenciamento que afetam a integridade, disponibilidade ou confidencialidade dos sistemas.
* **Conta Privilegiada:** Qualquer conta (humana ou não-humana) que possua acesso privilegiado.
* **Princípio do Menor Privilégio (PoLP):** Princípio de segurança que determina que um usuário deve possuir *apenas* as permissões mínimas necessárias para executar suas funções de trabalho, e nada mais.
* **PAM (Privileged Access Management):** Solução tecnológica (cofre de senhas, gerenciador de sessões) usada para proteger, gerenciar, controlar e auditar o acesso privilegiado.
* **Acesso Just-in-Time (JIT):** Modelo de concessão de acesso privilegiado de forma temporária, sob demanda, e revogado automaticamente após um período determinado.
* **MFA (Autenticação Multifator):** Método de autenticação que exige no mínimo dois fatores de verificação distintos.
* **Proprietário do Sistema (System Owner):** O indivíduo ou equipe responsável pela governança, segurança e funcionalidade de um ativo de informação.
* **Acesso Break-Glass:** Conta de acesso emergencial de altíssimo privilégio, usada apenas em cenários de desastre ou falha dos sistemas normais de autenticação.
* **Conta de Serviço:** Conta não-humana usada por aplicações, scripts ou serviços para interagir com outros sistemas.

## 4. Princípios Fundamentais de Segurança

1.  **Menor Privilégio (PoLP):** O acesso privilegiado é negado por padrão. Qualquer concessão deve ser justificada, aprovada e limitada ao mínimo necessário.
2.  **Acesso Não-Permanente:** O acesso privilegiado permanente é proibido. O modelo padrão é o **Acesso Just-in-Time (JIT)**.
3.  **Separação de Funções (SoD):** Funções críticas (ex: criar um usuário e atribuir permissões) devem ser segregadas entre diferentes indivíduos ou papéis.
4.  **Responsabilização (Accountability):** Todas as contas privilegiadas devem ser unicamente atribuídas a um indivíduo. Contas genéricas ou compartilhadas (`admin`, `root`) são estritamente proibidas para acesso humano interativo.
5.  **Rastreabilidade:** Todas as ações privilegiadas devem ser registradas, monitoradas e atribuídas a um indivíduo único.

## 5. Diretrizes da Política

### 5.1. Inventário e Classificação

Todas as contas privilegiadas em todos os sistemas devem ser identificadas, inventariadas e registradas na solução de PAM. Cada conta deve ter um `Proprietário do Sistema` designado.

### 5.2. Ciclo de Vida do Acesso (Solicitação e Aprovação)

1.  **Solicitação:** O acesso privilegiado deve ser solicitado formalmente através do sistema de ITSM (Service Desk), detalhando:
    * Identidade do solicitante.
    * Sistemas e nível de acesso.
    * Justificativa de negócio clara.
    * **Período de tempo (data de início e fim)** para o acesso (JIT).
2.  **Aprovação:** A solicitação deve ser aprovada formalmente (via sistema) pelo gestor direto do solicitante e pelo `Proprietário do Sistema`.
3.  **Rastreabilidade:** Todas as aprovações devem ser registradas e armazenadas para fins de auditoria.

### 5.3. Requisitos de Autenticação e Concessão

1.  **MFA Obrigatório:** A Autenticação Multifator é **mandatória** para todo e qualquer acesso privilegiado, sem exceções. Isso inclui acesso ao cofre PAM, VPN e acesso direto a plataformas de nuvem.
2.  **Contas Separadas:** Usuários devem possuir contas distintas:
    * **Conta Padrão:** Para atividades diárias (e-mail, navegação).
    * **Conta Privilegiada (`admin-nome.sobrenome`):** Usada *exclusivamente* para tarefas administrativas.
3.  **Solução PAM (Cofre de Senhas):**
    * O uso de uma solução PAM centralizada é **mandatório** para armazenar e gerenciar todas as credenciais privilegiadas (senhas, chaves SSH, chaves de API).
    * Credenciais **nunca** devem ser expostas ao usuário final. O acesso deve ser feito por *check-out* com rotação automática de senha após o uso, ou através de sessões seguras (proxy) iniciadas pelo PAM.
    * O armazenamento local de chaves privadas SSH ou credenciais em scripts é estritamente proibido.
4.  **Contas de Serviço:**
    * Credenciais de contas de serviço devem ser gerenciadas pela solução PAM.
    * A rotação automática de senhas para contas de serviço é mandatória e deve ser configurada com a maior frequência tecnicamente viável.

### 5.4. Monitoramento, Log e Auditoria

1.  **Monitoramento de Sessão:** Todas as sessões privilegiadas devem ser monitoradas. A **gravação de sessão (session recording)** deve ser habilitada sempre que tecnicamente viável.
2.  **Logs de Auditoria:** Logs detalhados (quem, o quê, quando, de onde) de todas as atividades privilegiadas devem ser gerados, protegidos contra adulteração e enviados a um sistema centralizado de **SIEM (Security Information and Event Management)**.
3.  **Alertas:** Alertas automáticos devem ser configurados no SIEM para atividades suspeitas (ex: acesso fora de horário, falhas de login, uso de contas `break-glass`).
4.  **Revisão de Logs:** A Equipe de Segurança da Informação (SOC) deve revisar ativamente os alertas e logs de acesso privilegiado.

### 5.5. Revisão e Revogação de Acesso

1.  **Atestado de Acesso (Revisão Periódica):** Os `Proprietários de Sistema` devem realizar uma revisão e atestado de todos os acessos privilegiados sob sua responsabilidade, no mínimo, **trimestralmente**. A falha em atestar resultará na revogação automática do acesso.
2.  **Revogação Imediata (Processo JML - Joiner, Mover, Leaver):**
    * O acesso privilegiado deve ser *automaticamente* revogado como parte do processo de desligamento (Leaver) de um colaborador.
    * O acesso deve ser reavaliado e, se necessário, revogado quando um colaborador muda de função (Mover).
    * O acesso JIT deve expirar e ser revogado automaticamente no final do período aprovado.

## 6. Processo de Acesso Emergencial (Break-Glass)

1.  Contas `break-glass` (ex: `aws-break-glass`) existem apenas para recuperação de desastres ou falha total do sistema de autenticação primário (ex: IdP).
2.  Essas contas devem ter senhas extremamente complexas, estar armazenadas no cofre PAM e exigir um processo de aprovação de múltiplos responsáveis para o *check-out*.
3.  O uso de uma conta `break-glass` deve disparar **alertas imediatos** para a equipe de Segurança da Informação e para o CISO.
4.  Qualquer uso exige uma justificativa formal *ex-post-facto* (após o fato) detalhando o incidente, as ações tomadas e o motivo do uso.
5.  A senha da conta `break-glass` deve ser rotacionada *automaticamente* pelo PAM imediatamente após o *check-in*.

## 7. Papéis e Responsabilidades

* **CISO:** Aprovador final da política e responsável pela governança de segurança.
* **Equipe de Segurança da Informação:** Gerenciar a solução PAM, monitorar atividades, responder a incidentes e conduzir auditorias de conformidade.
* **Proprietários de Sistema:** Aprovar solicitações de acesso e realizar os atestados de revisão trimestrais.
* **Equipe de TI / Infraestrutura:** Implementar e manter os controles técnicos (MFA, JIT) em conjunto com a Segurança.
* **Gestores:** Revisar e aprovar a necessidade de negócio para o acesso de suas equipes.
* **Usuários Privilegiados:** Cumprir esta política, proteger suas credenciais e reportar qualquer atividade suspeita.

## 8. Conformidade e Não-Cumprimento

O não-cumprimento desta política é considerado uma falha de segurança grave e será tratado com a máxima seriedade.

* Violações intencionais ou por negligência podem resultar em ações disciplinares, incluindo a rescisão do contrato de trabalho ou serviço, de acordo com as políticas de RH e a legislação aplicável.
* Falhas de processo identificadas em auditorias devem ser tratadas com um plano de ação e correção (PoA&M) formal.

## 9. Documentos de Referência

* Política Geral de Segurança da Informação (`POL-SEG-001`)
* Política de Gestão de Identidade e Acesso (IAM)
* Política de Gestão de Senhas
* Política de SIEM e Gerenciamento de Logs
* Procedimento de Resposta a Incidentes
