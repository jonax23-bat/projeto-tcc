# 📋 02. Especificação de Requisitos

## 1. Regras de Negócio (RN)

### RN01 - Cálculo de Estoque Preditivo
- Toda vez que uma dose for registrada com o status `Tomado`, o sistema subtrai a `quantidade_dose` do saldo em `quantidade_atual` no estoque.
- A fórmula de consumo diário é dada por:
  $$\text{Consumo Diário} = \left(\frac{24}{\text{intervalo\_horas}}\right) \times \text{quantidade\_dose}$$
- A estimativa de dias de cobertura é calculada por:
  $$\text{Dias Restantes} = \frac{\text{quantidade\_atual}}{\text{Consumo Diário}}$$

### RN02 - Gatilho de Alerta de Compra
- Quando $\text{Dias Restantes} \le \text{dias\_seguranca}$ (configurado pelo usuário/cuidador, padrão: 5 dias), o sistema deve emitir um alerta com prioridade alta para o Cuidador e/ou Paciente Independente indicando a necessidade de reposição.

### RN03 - Janela de Tolerância, Trava de Adiar (Snooze Lock) e Alerta ao Cuidador
- **Contagem Imutável a partir do Horário Original ($T_0$):** O cronômetro de segurança para notificação ao cuidador (ex.: 30 minutos) inicia no horário programado original ($T_0$) e **não é resetado ou estendido pelo botão "Adiar"**.
- **Limite Máximo de Adiamentos:** O botão "Adiar" só pode ser acionado **no máximo 2 vezes** por dose/sessão (ex.: 10 minutos cada) em qualquer modo. Na terceira tentativa, a opção de adiar é bloqueada.
- **Cancelamento do Alerta ao Cuidador:** O envio da notificação push de atraso/omissão ao cuidador **SÓ É CANCELADO se o botão "JÁ TOMEI" for acionado** antes de expirar a janela de $T_0 + 30\text{ min}$. Se o paciente adiar e não confirmar até $T_0 + 30\text{ min}$, o alerta é disparado pontualmente ao cuidador.

### RN04 - Permissões e Vínculos de Cuidado
- O perfil `Assistido` apenas visualiza e confirma doses diárias; não possui permissão para alterar prescrições ou estoques.
- O perfil `Cuidador` gerencia cadastros, receitas, compras de medicamentos e monitora os assistidos.
- O perfil `Independente` possui todas as funcionalidades unificadas para uso próprio.
- Um paciente assistido pode ter múltiplos cuidadores (ex.: filhos, cônjuges, enfermeiros).
- Um cuidador pode gerenciar múltiplos assistidos.

### RN05 - Agrupamento de Doses Simultâneas (Bandeja / Bloco de Horário)
- Se duas ou mais prescrições estiverem programadas para o mesmo horário (ex.: 08:00), o sistema **não** dispara múltiplos alarmes concorrentes.
- O sistema unifica as doses em uma única **Sessão de Medicação** (Bandeja Virtual), exibindo a lista consolidada com identificação visual distinta de cada medicamento e permitindo confirmação unitária ou global ("Tomei Todos").

### RN06 - Tratamentos Temporários e Ciclos com Contagem Regressiva
- Quando uma prescrição possuir `data_fim` ou duração fixa em dias (ex.: antibiótico por 7 dias ou analgésico pós-cirúrgico por 5 dias), o sistema deve exibir uma **barra de progresso / contagem regressiva** ("Dia 3 de 7").
- Ao atingir o último dia e a última dose confirmada, o sistema notifica a conclusão do tratamento e arquiva a prescrição automaticamente, encerrando os alarmes associados.

---

## 2. Requisitos Funcionais (RF)

| ID | Nome | Descrição | Atores |
|---|---|---|---|
| **RF01** | Autenticação e Cadastro | Permitir cadastro e login via e-mail/telefone e senha criptografada, com seleção de perfil inicial. | Todos |
| **RF02** | Gestão de Vínculos | Permitir que cuidadores convidem ou vinculem pacientes assistidos (idosos, filhos ou dependentes) através de código/QR code ou convite direto. | Cuidador, Assistido |
| **RF03** | Catálogo de Medicamentos | Manter catálogo de medicamentos (nome comercial, princípio ativo, formato: comprimido, gota, ml, suspensão, etc.). | Cuidador, Independente |
| **RF04** | Cadastro de Prescrição | Cadastrar receita médica com tipo (Contínuo vs. Temporário), horários, intervalo em horas, quantidade por dose, data de início e fim. | Cuidador, Independente |
| **RF05** | Controle de Estoque | Registrar quantidade de unidades compradas, saldo atual e margem de segurança em dias. | Cuidador, Independente |
| **RF06** | Alarme e Notificação de Dose | Emitir alertas visuais e sonoros no horário exato da medicação programada com suporte à Bandeja Virtual. | Assistido, Independente |
| **RF07** | Confirmação e Trava de Adiar | Disponibilizar botão de ação direta ("Já Tomei") e opção "Adiar 10 min" limitada a no máximo 2 repetições, mantendo a contagem ininterrupta de alerta ao cuidador. | Assistido, Independente |
| **RF08** | Alerta de Omissão ao Cuidador | Notificar cuidadores quando uma dose do assistido não for confirmada no tempo limite. | Cuidador |
| **RF09** | Alerta de Estoque Baixo | Notificar cuidadores e pacientes independentes quando o medicamento atingir o estoque mínimo. | Cuidador, Independente |
| **RF10** | Histórico e Relatórios | Exibir histórico de doses tomadas, atrasadas e esquecidas com taxas de adesão (%) e opção de exportação em PDF/CSV. | Cuidador, Independente |
| **RF11** | Painel Resumo Diário (Dashboard) | Exibir a linha do tempo do dia com todas as medicações e status em tempo real. | Cuidador, Independente |
| **RF12** | Gestão de Tratamentos Temporários | Exibir progresso de ciclos com término definido (ex: "Dia 4 de 10"), emitir alerta de conclusão de ciclo e arquivar automaticamente. | Todos |

---

## 3. Requisitos Não-Funcionais (RNF)

| ID | Categoria | Descrição |
|---|---|---|
| **RNF01** | **Acessibilidade** | A interface do Paciente Assistido deve cumprir diretrizes de acessibilidade (WCAG 2.1 AA), suporte a leitor de tela, tipografia de grande porte (mínimo 18sp/pt) e contraste mínimo de 4.5:1. |
| **RNF02** | **Usabilidade** | A ação de confirmação de dose no modo Assistido deve requerer no máximo 1 toque na tela (zero menus complexos). |
| **RNF03** | **Disponibilidade** | Os alarmes locais devem funcionar mesmo se o dispositivo estiver temporariamente sem conexão com a internet (offline-first para alarmes locais). |
| **RNF04** | **Segurança e Privacidade (LGPD)** | Dados sensíveis de saúde e senhas devem ser trafegados via HTTPS com TLS 1.3 e armazenados com hashing seguro (Argon2 ou bcrypt). |
| **RNF05** | **Tempo de Resposta** | O tempo de sincronização entre a confirmação da dose pelo paciente e a atualização do dashboard do cuidador deve ser inferior a 3 segundos (tempo real via WebSockets / Push Notifications). |
| **RNF06** | **Compatibilidade** | O aplicativo móvel deve rodar em dispositivos Android (versão 8.0+) e iOS (versão 14+), além de suporte opcional a Progressive Web App (PWA). |
| **RNF07** | **Resiliência e Sincronização Offline** | A atualização do consumo de medicamentos e o abatimento de estoque devem ser registrados localmente e garantidos de forma assíncrona (consistência eventual) imediatamente após a retomada da conexão de rede pelo dispositivo, impedindo perda de dados ou deduções duplicadas. |
