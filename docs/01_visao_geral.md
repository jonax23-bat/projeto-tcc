# 📄 01. Visão Geral e Escopo do Projeto

## 1. Contexto e Problema
O envelhecimento populacional e o aumento de doenças crônicas exigem tratamentos contínuos e rigorosos com múltiplos medicamentos diários (polifarmácia). 
Os principais desafios observados no dia a dia são:
1. **Esquecimentos e Inconsistência de Horários:** Dificuldade dos pacientes (especialmente idosos) em lembrar horários e dosagens corretas.
2. **Falta de Monitoramento Remoto:** Familiares e cuidadores frequentemente não sabem se o paciente realmente tomou o medicamento no horário programado.
3. **Ruptura de Estoque de Medicamentos:** O remédio acaba sem aviso prévio, gerando interrupção perigosa no tratamento contínuo.
4. **Interfaces Complexas:** A maioria dos aplicativos de saúde existentes possui excesso de menus e opções, tornando-se inacessível para idosos com limitações visuais ou cognitivas.

---

## 2. Proposta de Valor
Desenvolver uma plataforma/aplicativo móvel inteligente e colaborativo focado na adesão ao tratamento medicamentoso e na gestão preventiva de estoques de remédios, integrando **Paciente Assistido**, **Cuidador/Familiar** e **Paciente Independente** com interfaces dedicadas a cada necessidade.

---

## 3. Objetivos

### 3.1. Objetivo Geral
Desenvolver um sistema computacional para gestão de rotinas de medicação, rastreamento de adesão terapêutica em tempo real e controle automatizado de estoque doméstico com alertas preditivos de recompra.

### 3.2. Objetivos Específicos
- **Implementar interfaces adaptativas:** Criar uma interface simplificada (modo assistido/idoso) de alto contraste e foco em ação única ("Já Tomei"), e um dashboard gerencial para cuidadores.
- **Automatizar o controle de estoque:** Calcular a taxa de consumo diário e projetar a data de esgotamento do medicamento, disparando avisos quando o estoque atingir a margem de segurança.
- **Monitoramento em tempo real da adesão:** Notificar cuidadores quando uma dose não for confirmada dentro da janela de tolerância estabelecida.
- **Gerar relatórios de adesão:** Permitir a exportação/visualização do histórico de cumprimento das dosagens para consultas médicas.
- **Garantir relação N:N de cuidados:** Permitir que múltiplos cuidadores acompanhem um mesmo paciente e que um cuidador gerencie múltiplos assistidos.

---

## 4. Público-Alvo e Stakeholders
- **Foco Principal - Pacientes Idosos / Assistidos:** Usuários com doenças crônicas (polifarmácia) que necessitam de lembretes sonoros/visuais claros, interfaces de zero atrito e acompanhamento da família.
- **Cuidadores e Familiares:** Filhos, cônjuges ou enfermeiros que administram a rotina de idosos, além de **pais/mães administrando tratamentos infantis** (ex.: antibióticos por 7 a 10 dias para crianças).
- **Pacientes em Recuperação Pós-Operatória / Tratamentos Temporários:** Pessoas que passaram por cirurgias ou quadros agudos (infecções, inflamações) e precisam seguir um protocolo rigoroso de curta duração (ex.: analgésicos e antibióticos por 5 a 15 dias com contagem regressiva).
- **Pacientes Independentes (Autogerenciados):** Adultos com tratamentos contínuos ou suplementação que gerenciam a própria rotina.
- **Profissionais de Saúde (Secundário):** Médicos que avaliam relatórios de adesão ao tratamento contínuo ou o cumprimento integral de ciclos antibióticos.

---

## 5. Diferenciais Competitivos
| Característica | Aplicativos Comuns de Alarme | Sistema Proposto (TCC) |
|---|---|---|
| **Público Idoso** | Interfaces genéricas cheias de abas | Interface "Zero Atrito", botões gigantes e comandos diretos |
| **Estoque** | Sem estoque ou contagem manual | Cálculo automático baseado em prescrição e consumo real |
| **Alerta de Compra** | Não possui | Preditivo com base em dias restantes de segurança |
| **Monitoramento Familiar** | Individual / Local | Compartilhado (rede de cuidadores com alertas de omissão) |
| **Relatórios de Adesão** | Básicos ou inexistentes | Histórico com timestamps reais de confirmação |
