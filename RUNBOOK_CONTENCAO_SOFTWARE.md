# Procedimento de Resposta a Incidentes de Software (PRI-Software)
# Foco: Isolamento e Mitigação Rápida

Este documento descreve os passos imediatos para isolar e mitigar ameaças e vulnerabilidades críticas de software (ex: RCE, SQL Injection, Vazamento de Dados).

## 1. Responsáveis Imediatos

* **Líder de Incidente (Tech Lead / SRE):** [Nome ou Papel]
* **Comunicação (CTO / PO):** [Nome ou Papel]

---

## 2. Procedimentos de Isolamento (Ação Imediata)

O objetivo é parar a "sangria" imediatamente. Escolha a opção mais rápida e aplicável:

### Opção A: Isolamento via WAF / API Gateway
(Usado para XSS, SQLi, Request Smuggling)

1.  **Ação:** Criar uma regra de bloqueio emergencial (ex: bloquear IP, User-Agent ou padrão de URL) no nosso WAF (Ex: ModSecurity, Cloudflare, etc.).
2.  **Responsável:** [Equipe de SRE/DevOps]

### Opção B: Isolamento via Balanceador de Carga (Load Balancer)
(Usado para falha em um pod/servidor específico)

1.  **Ação:** Remover o(s) servidor(es) / pod(s) / container(s) afetados do pool do balanceador de carga (ex: Nginx, HAProxy, AWS ALB).
2.  **Responsável:** [Equipe de SRE/DevOps]

### Opção C: Isolamento via "Feature Flag" ou Configuração
(Usado para falha lógica em uma funcionalidade)

1.  **Ação:** Desabilitar a funcionalidade vulnerável via painel de Feature Flags ou alterando uma variável de ambiente (ex: `FEATURE_CHECKOUT_V2=false`).
2.  **Responsável:** [Equipe de Desenvolvimento]

### Opção D: Desativação de Endpoint (Código)
(Usado quando a rota inteira está comprometida)

1.  **Ação:** Comentar ou desabilitar a rota/endpoint vulnerável no código (ex: no `routes.rb`, `app.js`, `urls.py`) e fazer deploy emergencial.
2.  **Responsável:** [Equipe de Desenvolvimento]

---

## 3. Procedimentos de Mitigação (Correção)

1.  **Análise:** Com o sistema isolado, a equipe de desenvolvimento irá analisar a causa raiz (logs, APM, etc.).
2.  **Hotfix:** Desenvolver o *patch* de correção em um *branch* separado (ex: `hotfix/vulnerabilidade-xyz`).
3.  **Validação:** Testar a correção em ambiente de homologação/staging.
4.  **Deploy:** Fazer o deploy da correção em produção.
5.  **Reversão do Isolamento:** Remover as regras de bloqueio do Passo 2 (WAF, Feature Flags, etc.).

---

## 4. Atualização do Plano

Este documento é revisado a cada 6 meses ou após todo incidente crítico.
*Última revisão: DD/MM/AAAA*
