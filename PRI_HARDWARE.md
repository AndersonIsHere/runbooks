# Plano de Resposta a Incidentes (PRI) - Hardware
# Foco: Comprometimento de Ativos Físicos (Notebooks, Dispositivos Móveis)

## 1. Escopo e Objetivos

Este documento define os procedimentos para resposta a incidentes de segurança envolvendo hardware da Empresa Zukk. Os objetivos são:
1.  **Isolar** o dispositivo para prevenir danos maiores.
2.  **Proteger** os dados corporativos.
3.  **Recuperar** ou **Substituir** o ativo de forma segura.

## 2. Responsáveis
* **Usuário Afetado:** Primeiro a reportar.
* **TI Help Desk:** Ponto central de registro (via GLPI/Jira/Ticket).
* **Equipe de Segurança/Infra:** Execução de bloqueio, expurgo e análise.
* **Gestor do Usuário:** Aprovação de substituição, ciência do risco.

---

## 3. Procedimento: Infecção por Malware (Ransomware, Vírus)

Usado quando um notebook ou dispositivo apresenta comportamento malicioso.

### Ação Imediata (Usuário)
1.  **Isolar:** Desconectar o dispositivo da rede **IMEDIATAMENTE**.
    * Desconectar o cabo de rede (Ethernet).
    * Desligar o Wi-Fi.
    * Desligar o Bluetooth.
2.  **Não Desligar:** Não desligue o equipamento (a menos que seja Ransomware em criptografia ativa), pois isso pode apagar evidências da memória volátil.
3.  **Reportar:** Abrir um chamado no Help Desk com o título "URGENTE: Suspeita de Malware em Hardware".

### Ação da Equipe de TI
1.  **Registro:** Registrar o incidente na ferramenta de tickets (ex: GLPI).
2.  **Isolamento (EDR):** Aplicar a política de "Isolamento de Rede" na ferramenta de EDR (ex: Wazuh, SentinelOne, etc.), se o usuário não o fez.
3.  **Análise:** Coletar evidências (se necessário para forense) ou mover para o procedimento de formatação.
4.  **Mitigação:** Formatar o dispositivo (re-image) a partir de uma imagem limpa.
5.  **Devolução:** Entregar o dispositivo formatado ao usuário.

---

## 4. Procedimento: Roubo ou Furto (Ato Malicioso Confirmado)

Usado quando o dispositivo foi subtraído de forma criminosa.

### Ação Imediata (Usuário)
1.  **Segurança Pessoal:** Garantir sua segurança física primeiro.
2.  **Boletim de Ocorrência (B.O.):** Registrar um B.O. junto às autoridades policiais. Este é um **passo obrigatório**.
3.  **Reportar:** Informar seu Gestor e abrir um chamado no Help Desk com o título "CRÍTICO: Furto/Roubo de Notebook [Modelo/Tag]" e anexar o B.O.

### Ação da Equipe de TI
1.  **Bloqueio Remoto:** Utilizar a ferramenta de MDM/Gestão (ex: Intune, Jamf, Google Workspace) para aplicar o **bloqueio total** do dispositivo.
2.  **Expurgo Remoto (Wipe):** Iniciar o comando de **expurgo remoto** (limpeza total) dos dados.
3.  **Troca de Senhas:** Forçar a redefinição de senha da conta do usuário (Active Directory, Google Workspace, etc.).
4.  **Avaliação de Impacto:** Avaliar quais dados sensíveis estavam no dispositivo para notificar as partes afetadas (se necessário).
5.  **Substituição:** Iniciar o fluxo de substituição do ativo.

---

## 5. Procedimento: Perda ou Extravio (Não Criminosa)

Usado quando o usuário não sabe onde o dispositivo está (ex: esquecido em táxi, aeroporto).

### Ação Imediata (Usuário)
1.  **Reportar:** Informar seu Gestor e abrir um chamado **IMEDIATAMENTE** no Help Desk com o título "ALERTA: Perda/Extravio de Notebook [Modelo/Tag]".

### Ação da Equipe de TI
1.  **Tentativa de Rastreio (Opcional):** Tentar localizar o dispositivo via MDM (se a função estiver habilitada).
2.  **Bloqueio Remoto:** Aplicar o **bloqueio total** do dispositivo via MDM (Medida de precaução imediata).
3.  **Troca de Senhas:** Forçar a redefinição de senha da conta do usuário.
4.  **Expurgo Remoto (Wipe):** Se o dispositivo não for localizado em um curto período (ex: 2 horas), tratar como "Roubo" e iniciar o **expurgo remoto** (Wipe).
5.  **Avaliação de Impacto:** Avaliar o risco de exposição de dados.

---

## 6. Revisão do Plano

Este documento é revisado a cada 12 meses ou após todo incidente crítico de hardware.
   *Última revisão: 16/02/2025*
