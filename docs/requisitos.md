# Requisitos e Histórias de Usuário — Instituto Muay Thai do Bem

Este documento reúne os requisitos do CRM do Instituto Muay Thai do Bem em 35 histórias de usuário, organizadas pelos pilares do documento de estruturação da ONG, e 8 requisitos não funcionais. Cada história vira uma issue no GitHub com a etiqueta da sua fase.

**Como ler cada história**

- **História:** *Como [persona], quero [ação], para [benefício].*
- **Critério de aceite:** comportamento verificável no formato *Dado / Quando / Então*, com o cenário negativo quando houver. A história só está pronta quando todos os critérios passam.
- **Nota técnica:** como a solução será construída. Pode mudar sem mudar a história.
- **Fase / Prioridade:** fase do plano de ação (0 a 7) e prioridade MoSCoW (**Must**: sem ela o projeto não entrega; **Should**: importante, mas pode ir para v2; **Could**: desejável).

---

## Personas

| Persona | Licença | Permission Set Group | O que vê |
| --- | --- | --- | --- |
| Admin | Salesforce | System Administrator | Tudo |
| Diretor(a) (inclui Presidente e Diretor Financeiro) | Salesforce | `MTB_Gestao` + `MTB_Captacao` | Tudo, somente leitura em configurações |
| Coordenador(a) de núcleo | Salesforce Platform | `MTB_Programa` | Jovens, aulas, presenças e despesas do próprio núcleo |
| Captação (responsável por captação) | Salesforce Platform | `MTB_Captacao` | Doadores, oportunidades, campanhas; nenhum dado escolar ou de saúde |
| Voluntário | Experience Cloud | Perfil do portal | Os próprios turnos e horas |

**Destinatários sem login:** Padrinho/Doador, Membro de Conselho, Patrocinador (empresa) e Responsável pelo jovem. Eles recebem e-mails ou relatórios, mas não acessam a org. O Instrutor é um Contact (lookup em `Aula__c`) e também não tem usuário.

---

## Resumo do backlog

| ID | História (resumo) | Pilar | Fase | Prioridade |
| --- | --- | --- | --- | --- |
| US01 | Cadastrar diretoria e conselhos com papéis | 01 Governança | 1 | Must |
| US02 | Registrar despesas do núcleo | 01 Governança | 1 | Must |
| US03 | Aprovar despesas por alçada (R$ 2 mil / R$ 10 mil) | 01 Governança | 3 | Must |
| US04 | Declaração anual de conflito de interesses | 01 Governança | 3 | Should |
| US05 | KPI taxa de retenção anual | 02 Impacto | 4 | Must |
| US06 | KPI % com ensino médio completo | 02 Impacto | 4 | Must |
| US07 | KPI % de ingressantes no ensino superior | 02 Impacto | 4 | Must |
| US08 | KPI % inseridos no mercado formal | 02 Impacto | 4 | Must |
| US09 | KPI instrutores formados por ano | 02 Impacto | 4 | Should |
| US10 | KPI famílias engajadas | 02 Impacto | 4 | Should |
| US11 | KPI custo por beneficiário/mês | 02 Impacto | 4 | Must |
| US12 | Painel de Impacto com assinatura mensal | 02 Impacto | 4 | Must |
| US13 | Painel do Núcleo (dinâmico) | 02 Impacto | 4 | Should |
| US14 | Doações recorrentes por nível + campanha de apadrinhamento | 03 Financeiro | 2 | Must |
| US15 | Vincular padrinho ao jovem apadrinhado | 03 Financeiro | 2 | Must |
| US16 | Funis de patrocínio, edital e Lei de Incentivo | 03 Financeiro | 2 | Must |
| US17 | Alocar receita por núcleo (GAU) | 03 Financeiro | 2 | Must |
| US18 | Painel de Captação (meta R$ 236 mil) | 03 Financeiro | 4 | Must |
| US19 | Painel do Patrocinador por núcleo | 03 Financeiro | 4 | Should |
| US20 | Cadastrar núcleos e grade de aulas | 04 Esporte | 1 | Must |
| US21 | Matrícula guiada de novo jovem | 04 Esporte | 3 | Must |
| US22 | Certificação CBMT atualiza a etapa da trilha | 04 Esporte | 1 e 3 | Must |
| US23 | Frequência de treino 30 dias e risco de evasão | 04 Esporte | 3 e 5 | Must |
| US24 | Chamada da turma inteira pelo celular | 04 Esporte | 5 | Should |
| US25 | Acompanhamento escolar mensal | 05 Educação | 1 e 3 | Must |
| US26 | Alerta de frequência escolar abaixo de 75% | 05 Educação | 3 | Must |
| US27 | Jornada educacional, egressos e vínculos | 05 Educação | 1 | Must |
| US28 | Linha do tempo da jornada na página do jovem | 05 Educação | 5 | Could |
| US29 | E-mail de boas-vindas na primeira doação | Power of Us | 3 | Should |
| US30 | Relatório trimestral ao padrinho | Power of Us | 3 | Must |
| US31 | Portal do voluntário com onboarding | Power of Us | 6 | Should |
| US32 | Inscrição em turnos e registro de horas | Power of Us | 6 | Should |
| US33 | Coordenador vê apenas o próprio núcleo | Segurança | 1 | Must |
| US34 | Captação não vê dados escolares e de saúde | Segurança | 1 | Must |
| US35 | Validações de qualidade nos dados do jovem | Segurança | 1 | Must |

---

## Pilar 01 — Governança

### US01 — Cadastrar diretoria e conselhos
**História:** Como Admin, quero cadastrar os membros da diretoria e dos conselhos com seus papéis, para mapear quem responde por cada decisão da ONG.

**Critério de aceite**
- Dado um Contact com Record Type Membro de Conselho, quando eu criar uma Affiliation com a organização "Instituto Muay Thai do Bem", então posso escolher o papel (Presidente, Diretor Financeiro, Conselheiro Fiscal, Conselheiro Consultivo) e informar data de início e fim.
- Dado um membro com Affiliation de status Atual, quando eu abrir a conta da ONG, então ele aparece na lista de afiliações ativas.

**Nota técnica:** Contact (RT Membro de Conselho) + Affiliation (NPSP); picklist de papel na Affiliation.
**Fase:** 1 · **Prioridade:** Must

### US02 — Registrar despesas do núcleo
**História:** Como Coordenador(a) de núcleo, quero registrar as despesas do meu núcleo, para manter o controle financeiro por unidade.

**Critério de aceite**
- Dado que sou coordenador(a) de Taboão, quando eu criar uma Despesa com competência, categoria e valor, então ela fica vinculada ao núcleo Taboão.
- Dado que sou coordenador(a) de Taboão, quando eu listar despesas, então não vejo as despesas de Butantã.

**Nota técnica:** `Despesa__c` com lookup obrigatório para `Nucleo__c`; base do KPI de custo por beneficiário (US11).
**Fase:** 1 · **Prioridade:** Must

### US03 — Aprovar despesas por alçada
**História:** Como Diretor(a) Financeiro(a), quero aprovar previamente despesas acima de R$ 2 mil, e que as acima de R$ 10 mil também passem pelo(a) Presidente, para garantir responsabilidade orçamentária.

**Critério de aceite**
- Dada uma despesa de R$ 1.500, quando ela for salva, então não entra em aprovação.
- Dada uma despesa de R$ 3.000, quando for submetida, então vai para aprovação do(a) Diretor(a) Financeiro(a) e fica bloqueada para edição até a decisão.
- Dada uma despesa de R$ 12.000, quando o(a) Diretor(a) Financeiro(a) aprovar, então ela segue para o(a) Presidente; só fica Aprovada depois das duas aprovações.
- Dada uma despesa rejeitada, então o(a) coordenador(a) recebe a notificação com o motivo.

**Nota técnica:** Approval Process `MTB_Aprovacao_Alcada` em `Despesa__c`, com 2 etapas. Limiares em `MTB_Parametro__mdt`.
**Fase:** 3 · **Prioridade:** Must

### US04 — Declaração anual de conflito de interesses
**História:** Como Diretor(a), quero que todo membro de conselho ativo tenha uma declaração de conflito de interesses pendente a cada ano, com lembrete por e-mail, para manter a conformidade da ONG.

**Critério de aceite**
- Dados 12 membros com Affiliation ativa, quando o fluxo anual rodar, então são criadas 12 `Declaracao_Conflito__c` com status Pendente para o ano corrente, e cada membro recebe o e-mail de lembrete.
- Dado um membro que já tem declaração do ano corrente, quando o fluxo rodar de novo, então não é criada uma segunda declaração.
- Dado um membro com Affiliation encerrada, então nenhuma declaração é criada para ele.
- Quando o Admin registrar a data de assinatura, então a declaração passa para Assinada.

**Nota técnica:** Scheduled Flow `MTB_Declaracao_Conflito_Anual`; Lightning Email Template de lembrete.
**Fase:** 3 · **Prioridade:** Should

---

## Pilar 02 — Impacto

Todas as histórias deste pilar usam os dados fictícios carregados nas fases 1 e 2. Cada KPI tem um relatório próprio, testado antes de entrar em um painel.

### US05 — KPI taxa de retenção anual (meta > 80%)
**História:** Como Diretor(a), quero acompanhar a taxa de retenção anual dos jovens, para medir se as turmas se sustentam.

**Critério de aceite**
- Dado o snapshot mensal de jovens ativos, quando eu abrir o relatório, então vejo um gráfico de linha com os ativos mês a mês.
- Dados 30 ativos no início do período e 3 saídas com `Data_Saida__c` no período, então a retenção exibida é 90% e o status aparece como dentro da meta.

**Nota técnica:** Reporting Snapshot mensal + `Data_Saida__c`.
**Fase:** 4 · **Prioridade:** Must

### US06 — KPI % com ensino médio completo (meta 100%)
**História:** Como Diretor(a), quero saber quantos jovens elegíveis concluíram o ensino médio, para medir o impacto educacional.

**Critério de aceite**
- Dado que só entram no cálculo jovens com idade para ter concluído o ensino médio (18 anos ou mais), quando eu abrir o relatório, então vejo um gauge com o percentual sobre esses elegíveis.
- Um jovem de 15 anos com nível Fundamental não reduz o percentual.

**Nota técnica:** `Nivel_Escolar__c` + data de nascimento; filtro de elegibilidade por idade.
**Fase:** 4 · **Prioridade:** Must

### US07 — KPI % de ingressantes no ensino superior (meta > 30%)
**História:** Como Diretor(a), quero saber quantos jovens e egressos chegaram ao ensino superior e em quais cursos, para medir o acesso à universidade.

**Critério de aceite**
- Quando eu abrir o relatório, então vejo um gauge com o percentual de jovens com nível Superior em curso ou Superior completo, e a lista dos cursos.
- Dado um jovem com nível Superior e `Curso_Superior__c` vazio, então o registro não pode ser salvo (ver US35).

**Nota técnica:** `Nivel_Escolar__c` + `Curso_Superior__c`.
**Fase:** 4 · **Prioridade:** Must

### US08 — KPI % inseridos no mercado formal (meta > 40%)
**História:** Como Diretor(a), quero saber quantos egressos e jovens maiores de 16 anos estão no mercado formal, para medir a empregabilidade gerada pelo programa.

**Critério de aceite**
- Dado o grupo de egressos e jovens com mais de 16 anos, quando eu abrir o relatório, então vejo um donut por `Situacao_Profissional__c` e o percentual de CLT + Estágio sobre o grupo.
- Jovens com 16 anos ou menos não entram no cálculo.

**Nota técnica:** `Situacao_Profissional__c`, `Status_Programa__c` = Egresso, data de nascimento.
**Fase:** 4 · **Prioridade:** Must

### US09 — KPI instrutores formados por ano (meta 5)
**História:** Como Diretor(a), quero saber quantos jovens se formaram instrutores no ano, para medir a formação de multiplicadores.

**Critério de aceite**
- Dadas certificações CBMT de etapa Instrutor com data de conclusão no ano corrente, quando eu abrir o relatório, então vejo a contagem e o status contra a meta de 5.
- Certificações de anos anteriores não entram na contagem.

**Nota técnica:** Custom Report Type Jovem com Certificações; filtro Etapa = Instrutor e Data de conclusão = este ano.
**Fase:** 4 · **Prioridade:** Should

### US10 — KPI famílias engajadas (meta +60)
**História:** Como Diretor(a), quero saber quantas famílias participam do programa, para avaliar o impacto na comunidade.

**Critério de aceite**
- Quando eu abrir o relatório, então vejo o número de Households com pelo menos 1 jovem ativo ou 1 responsável ativo.
- Uma família cujos jovens são todos Inativos não é contada.

**Nota técnica:** Account (Household) com Contacts; métrica no painel.
**Fase:** 4 · **Prioridade:** Should

### US11 — KPI custo por beneficiário/mês (meta < R$ 350)
**História:** Como Diretor(a), quero ver o custo mensal por beneficiário de cada núcleo, para usar melhor os recursos recebidos.

**Critério de aceite**
- Dadas despesas de R$ 4.500 em Taboão no mês e 15 jovens ativos em Taboão, quando eu abrir o relatório, então o custo exibido para Taboão é R$ 300 e o status aparece como dentro da meta.
- Os valores são exibidos separados por núcleo.

**Nota técnica:** Custom Report Type Núcleo com Despesas e Jovens; fórmula de resumo (soma de `Despesa__c.Valor` ÷ jovens ativos).
**Fase:** 4 · **Prioridade:** Must

### US12 — Painel de Impacto com assinatura mensal
**História:** Como Diretor(a), quero um Painel de Impacto com os 7 KPIs e recebê-lo por e-mail todo mês, para apresentar aos conselhos e patrocinadores sem precisar entrar no sistema.

**Critério de aceite**
- Quando eu abrir o "Painel de Impacto", então vejo os 7 KPIs (US05 a US11), cada um com valor, meta e status.
- Dada a assinatura mensal ativa, então recebo o painel por e-mail no primeiro dia útil do mês.

**Nota técnica:** Dashboard + assinatura (Subscribe).
**Fase:** 4 · **Prioridade:** Must

### US13 — Painel do Núcleo
**História:** Como Coordenador(a) de núcleo, quero um painel com a frequência de treino, os jovens em risco e as próximas aulas do meu núcleo, para agir no dia a dia.

**Critério de aceite**
- Dado que sou coordenador(a) de Butantã, quando eu abrir o painel, então vejo só os dados de Butantã.
- Dado que sou coordenador(a) de Taboão, quando eu abrir o mesmo painel, então vejo só os dados de Taboão.

**Nota técnica:** Dashboard dinâmico ("executar como usuário logado") para respeitar o sharing.
**Fase:** 4 · **Prioridade:** Should

---

## Pilar 03 — Financeiro e Captação

### US14 — Doações recorrentes por nível e campanha de apadrinhamento
**História:** Como Captação, quero registrar doações mensais recorrentes por nível e ligá-las à campanha de apadrinhamento, para prever a receita recorrente e medir o resultado da campanha.

**Critério de aceite**
- Quando eu criar um Recurring Donation, então escolho o nível: Apoiador (R$ 50), Parceiro (R$ 100), Padrinho (R$ 200) ou Patrono (R$ 500), e as parcelas futuras são geradas automaticamente.
- Dada a Campaign "Apadrinhamento 2027", quando um doador for incluído, então tem status de membro (Enviado, Respondeu, Doou).

**Nota técnica:** Recurring Donation (NPSP) + `Nivel_Apadrinhamento__c`; Campaign com hierarquia por ano.
**Fase:** 2 · **Prioridade:** Must

### US15 — Vincular padrinho ao jovem apadrinhado
**História:** Como Captação, quero ligar a doação de um padrinho ao jovem que ele apoia, para personalizar a prestação de contas.

**Critério de aceite**
- Quando eu preencher o jovem apadrinhado no Recurring Donation, então a busca só mostra Contacts com Record Type Jovem.
- Dado o vínculo feito, quando eu abrir o jovem, então vejo quem é o padrinho dele.

**Nota técnica:** `Jovem_Apadrinhado__c` (lookup Contact) com lookup filter por Record Type.
**Fase:** 2 · **Prioridade:** Must

### US16 — Funis de patrocínio, edital e Lei de Incentivo
**História:** Como Captação, quero acompanhar patrocínios, editais e projetos de Lei de Incentivo, cada um com suas etapas, para saber em que ponto está cada negociação ou submissão.

**Critério de aceite**
- Dada uma Opportunity de Patrocínio de Núcleo, então as etapas são: Prospecção → Proposta enviada → Negociação → Fechado ganho/perdido; e informo nível (Apoiador Corporativo R$ 2 mil, Parceiro de Núcleo R$ 5 mil, Master R$ 10 mil), núcleo patrocinado e contrapartidas.
- Dado um Edital, então as etapas são: Identificado → Em elaboração → Submetido → Aprovado → Em execução → Prestação de contas.
- Dada uma Lei de Incentivo, então as etapas são: Projeto submetido → Aprovado no Ministério → Captação → Executado.
- Um Edital não mostra as etapas de Patrocínio, e vice-versa.

**Nota técnica:** Opportunity Record Types + Sales Processes; campos Nível, `Nucleo_Patrocinado__c`, Contrapartidas.
**Fase:** 2 · **Prioridade:** Must

### US17 — Alocar receita por núcleo
**História:** Como Captação, quero alocar cada doação a um núcleo (Taboão, Butantã ou Geral), para garantir que a verba vá para o lugar certo e prestar contas.

**Critério de aceite**
- Dada uma doação fechada sem alocação específica, então ela é alocada automaticamente ao GAU Geral.
- Dado um patrocínio de núcleo com núcleo patrocinado Taboão, quando eu alocar, então 100% vai para o GAU Taboão.
- O relatório de alocações soma as receitas por núcleo.

**Nota técnica:** General Accounting Units (NPSP): um por núcleo + Geral; alocação padrão.
**Fase:** 2 · **Prioridade:** Must

### US18 — Painel de Captação
**História:** Como Captação, quero um painel com a receita recorrente mensal, o pipeline de editais e a meta do ano, para saber se vamos atingir os R$ 236 mil.

**Critério de aceite**
- Quando eu abrir o painel, então vejo: receita recorrente mensal, pipeline de editais por etapa e meta anual de R$ 236 mil contra o realizado (Opportunities Fechado ganho no ano).

**Nota técnica:** Dashboard sobre Opportunities e Recurring Donations.
**Fase:** 4 · **Prioridade:** Must

### US19 — Painel do Patrocinador
**História:** Como Captação, quero gerar um painel filtrado pelo núcleo que uma empresa patrocina, para enviar à empresa como base do relatório de sustentabilidade (ESG) dela.

**Critério de aceite**
- Quando eu filtrar o painel por Taboão, então todos os componentes mostram só dados de Taboão.
- O painel não exibe nome, dados escolares ou de saúde de nenhum jovem, apenas números agregados.

**Nota técnica:** Dashboard com filtro por núcleo; exportado ou enviado pela Captação (o patrocinador não tem login).
**Fase:** 4 · **Prioridade:** Should

---

## Pilar 04 — Esporte

### US20 — Cadastrar núcleos e grade de aulas
**História:** Como Coordenador(a) de núcleo, quero cadastrar as aulas do meu núcleo com data, horário, instrutor e nível, para organizar a capacidade das turmas.

**Critério de aceite**
- Dado um núcleo com endereço, coordenador(a), capacidade e status Ativo, quando eu criar uma Aula, então ela pertence obrigatoriamente a um núcleo.
- O instrutor escolhido na aula é um Contact.
- Quando um núcleo for apagado, então suas aulas também são (master-detail).

**Nota técnica:** `Nucleo__c` (Admin cadastra) e `Aula__c` master-detail de `Nucleo__c`.
**Fase:** 1 · **Prioridade:** Must

### US21 — Matrícula guiada de novo jovem
**História:** Como Coordenador(a) de núcleo, quero matricular um jovem por um formulário guiado, para criar família, jovem, responsável e primeiro acompanhamento de uma vez.

**Critério de aceite**
- Quando eu clicar em "Nova matrícula" e preencher as telas, então são criados: Household, Contact Jovem (núcleo, data de ingresso, etapa da jornada Ingresso, etapa da trilha Iniciante), Contact Responsável, Relationship Responsável ↔ Jovem e o primeiro Acompanhamento Escolar.
- Se algum passo falhar, então nada é gravado pela metade e vejo uma mensagem de erro clara.

**Nota técnica:** Screen Flow `MTB_Matricula_Jovem` com fault path.
**Fase:** 3 · **Prioridade:** Must

### US22 — Certificação CBMT atualiza a etapa da trilha
**História:** Como Coordenador(a) de núcleo, quero registrar a certificação de um jovem em uma etapa da trilha CBMT, para documentar o avanço esportivo.

**Critério de aceite**
- Quando eu criar uma `Certificacao_CBMT__c` com etapa, data de conclusão, graduador e validade, então ela aparece na página do jovem.
- Dada uma certificação de etapa Atleta para um jovem que estava em Intermediário, quando ela for salva, então `Etapa_Trilha__c` do jovem passa para Atleta e o Path na página do jovem reflete a mudança.
- Uma certificação de etapa inferior à atual não rebaixa o jovem.

**Nota técnica:** `Certificacao_CBMT__c` master-detail de Contact (Fase 1). Atualização da etapa: Record-Triggered Flow `MTB_Atualiza_Etapa_Trilha` (Fase 3). **Esta automação não consta no catálogo do plano e deve ser incluída.** Path sobre `Etapa_Trilha__c` no Contact.
**Fase:** 1 e 3 · **Prioridade:** Must

### US23 — Frequência de treino 30 dias e risco de evasão
**História:** Como Coordenador(a) de núcleo, quero ver a frequência de treino dos últimos 30 dias de cada jovem e que o jovem sem presença há 30 dias seja marcado como "Em risco" com uma tarefa para mim, para agir antes do abandono.

**Critério de aceite**
- Dado um jovem ativo cuja última presença foi há 31 dias, quando a rotina diária rodar, então `Status_Programa__c` vira "Em risco" e é criada uma Task para o(a) coordenador(a) do núcleo: "Contatar a família".
- Dado um jovem com presença há 10 dias, então o status não muda.
- Dado um jovem já "Em risco", quando a rotina rodar de novo, então não é criada uma Task duplicada.
- `Frequencia_Treino_30d__c` e `Ultima_Presenca__c` estão atualizados todo dia.

**Nota técnica:** Versão 1 (Fase 3): Scheduled Flow `MTB_Risco_Evasao`. Versão 2 (Fase 5): Apex Batch + Schedulable `MTB_CalculoIndicadoresBatch`, que passa a calcular frequência e risco; ao ativá-lo, o Flow é desativado para não haver duas automações gravando o mesmo campo. Registrar no ADR 003. Limiar de 30 dias em `MTB_Parametro__mdt`.
**Fase:** 3 e 5 · **Prioridade:** Must

### US24 — Chamada da turma inteira pelo celular
**História:** Como Coordenador(a) de núcleo, quero registrar a presença da turma inteira em uma tela pelo celular, para não atrasar o início do treino.

**Critério de aceite**
- Quando eu abrir uma aula, então vejo a lista de jovens ativos do núcleo e marco Presente, Falta ou Justificada para cada um, salvando tudo de uma vez.
- Dado um jovem que já tem presença nessa aula, quando eu tentar registrar de novo, então o sistema impede a duplicidade e mostra uma mensagem.
- A tela funciona no app móvel do Salesforce.

**Nota técnica:** LWC `mtbChamada` + Apex; `PresencaTrigger` com `PresencaTriggerHandler` validando duplicidade em `Presenca__c` (junção Aula × Contact).
**Fase:** 5 · **Prioridade:** Should

---

## Pilar 05 — Educação

### US25 — Acompanhamento escolar mensal
**História:** Como Coordenador(a) de núcleo, quero registrar todo mês a frequência escolar, a média e as disciplinas críticas de cada jovem, para cumprir o eixo educacional do programa.

**Critério de aceite**
- Quando eu criar um `Acompanhamento_Escolar__c` com mês de referência, frequência (%), média, disciplinas críticas e observações, então ele aparece no histórico do jovem.
- Dado um novo acompanhamento salvo, então `Frequencia_Escolar__c` do jovem passa a mostrar a frequência desse acompanhamento mais recente.
- Não é possível registrar dois acompanhamentos do mesmo jovem para o mesmo mês.

**Nota técnica:** `Acompanhamento_Escolar__c` master-detail de Contact (Fase 1); a atualização do campo no jovem fica no mesmo Flow da US26 (Fase 3); a regra de duplicidade pode ser validada por campo único (Contact + mês).
**Fase:** 1 e 3 · **Prioridade:** Must

### US26 — Alerta de frequência escolar abaixo de 75%
**História:** Como Coordenador(a) de núcleo, quero receber um alerta e uma tarefa quando a frequência escolar de um jovem ficar abaixo de 75%, para acionar a família imediatamente.

**Critério de aceite**
- Dado um jovem ativo de Taboão, quando um acompanhamento for salvo com frequência de 70%, então o(a) coordenador(a) de Taboão recebe uma Task e um e-mail, e o status do jovem vira "Em risco".
- Dado um acompanhamento com frequência de 80%, então nenhuma Task ou e-mail é gerado.
- Se o limiar for alterado para 80% no Custom Metadata, então uma frequência de 78% passa a gerar o alerta, sem editar o Flow.

**Nota técnica:** Record-Triggered Flow (after save) `MTB_Alerta_Frequencia_Escolar`; Lightning Email Template; limiar em `MTB_Parametro__mdt`.
**Fase:** 3 · **Prioridade:** Must

### US27 — Jornada educacional, egressos e vínculos
**História:** Como Coordenador(a) de núcleo, quero registrar a etapa da jornada educacional, o nível escolar, a situação profissional e os vínculos do jovem com escola, universidade e mentor, para acompanhar o jovem até depois de sair do programa.

**Critério de aceite**
- Cada jovem tem etapa da jornada (Ingresso, Acompanhamento, Orientação, Acesso superior, Empregabilidade, Egresso), nível escolar e situação profissional.
- Quando um jovem sair do programa, então registro a data de saída e o status Egresso, e ele continua aparecendo nos KPIs de egressos (US07, US08).
- O vínculo com escola ou universidade é registrado como Affiliation; o vínculo com mentor, como Relationship recíproco.

**Nota técnica:** Campos `Etapa_Jornada__c`, `Nivel_Escolar__c`, `Situacao_Profissional__c`, `Data_Saida__c`; Affiliation e Relationship (NPSP).
**Fase:** 1 · **Prioridade:** Must

### US28 — Linha do tempo da jornada na página do jovem
**História:** Como Coordenador(a) de núcleo, quero ver na página do jovem o progresso na trilha CBMT e a linha do tempo educacional, para ter a visão completa em segundos.

**Critério de aceite**
- Quando eu abrir um jovem, então vejo as etapas da trilha (concluídas e atual) e os eventos educacionais em ordem cronológica.
- Para um jovem sem certificações, o componente mostra "Iniciante" sem erro.

**Nota técnica:** LWC `mtbJornadaJovem` na Lightning Record Page do Jovem.
**Fase:** 5 · **Prioridade:** Could

---

## Power of Us — Voluntários e comunicação com doadores

### US29 — E-mail de boas-vindas na primeira doação
**História:** Como Captação, quero que todo doador receba automaticamente um e-mail de agradecimento na primeira doação, para que ele se sinta parte do projeto desde o início.

**Critério de aceite**
- Dado um Contact sem doações anteriores, quando a primeira Opportunity dele for para Fechado ganho, então ele recebe o e-mail de boas-vindas e é incluído na campanha vigente.
- Dado um Contact que já tinha doação fechada, quando uma nova doação fechar, então nenhum e-mail de boas-vindas é enviado.

**Nota técnica:** Record-Triggered Flow `MTB_Boas_Vindas_Doador`; Lightning Email Template.
**Fase:** 3 · **Prioridade:** Should

### US30 — Relatório trimestral ao padrinho
**História:** Como Captação, quero que cada padrinho receba a cada 3 meses um e-mail com o avanço do jovem que apoia, para mostrar o resultado da contribuição dele.

**Critério de aceite**
- Dado um Recurring Donation ativo com jovem apadrinhado, quando o fluxo trimestral rodar, então o padrinho recebe e-mail com o primeiro nome do jovem, a etapa da trilha CBMT e a situação escolar resumida.
- Dado um Recurring Donation encerrado, então nenhum e-mail é enviado.
- O e-mail não traz notas, dados de saúde, endereço ou sobrenome do jovem.

**Nota técnica:** Scheduled Flow `MTB_Relatorio_Trimestral_Padrinho`; Lightning Email Template com merge fields.
**Fase:** 3 · **Prioridade:** Must

### US31 — Portal do voluntário com onboarding
**História:** Como Voluntário, quero um portal com login, página de boas-vindas e materiais de capacitação, para me preparar antes de atuar nos núcleos.

**Critério de aceite**
- Quando eu fizer login no portal, então vejo as páginas: boas-vindas, próximos turnos, minhas horas e materiais.
- Não vejo nenhum dado de jovens.

**Nota técnica:** Experience Cloud (template Build Your Own LWR ou Customer Service); perfil do portal.
**Fase:** 6 · **Prioridade:** Should

### US32 — Inscrição em turnos e registro de horas
**História:** Como Voluntário, quero me inscrever em turnos abertos e acompanhar minhas horas pelo portal, para contabilizar meu apoio.

**Critério de aceite**
- Quando eu me inscrever em um turno aberto, então ele aparece em "próximos turnos".
- Depois de concluído o turno, então as horas aparecem somadas em "minhas horas".
- Não vejo turnos nem horas de outros voluntários.

**Nota técnica:** Volunteers for Salesforce (V4S) ou `Turno_Voluntario__c` próprio (decidir em ADR); Sharing Sets.
**Fase:** 6 · **Prioridade:** Should

---

## Segurança e acesso (transversal)

### US33 — Coordenador vê apenas o próprio núcleo
**História:** Como Diretor(a), quero que cada coordenador(a) veja apenas os jovens, aulas, presenças e despesas do próprio núcleo, para proteger dados de menores e evitar erros operacionais.

**Critério de aceite**
- Dado que estou logado(a) como coordenador(a) de Taboão (*Login As*), quando eu listar jovens, então vejo os 15 jovens de Taboão e nenhum de Butantã.
- Dado que estou logado(a) como Diretor(a), então vejo os 30 jovens.
- O roteiro "posso / não posso" de cada persona está registrado em `docs/seguranca.md`.

**Nota técnica:** OWD Contact e Account Private, `Nucleo__c` Public Read Only; Role Hierarchy (Diretoria → Coordenação Taboão / Butantã; Diretoria → Captação); Sharing Rules por critério de núcleo; Permission Set Groups.
**Fase:** 1 · **Prioridade:** Must

### US34 — Captação não vê dados escolares e de saúde
**História:** Como Diretor(a), quero que a equipe de Captação não veja dados escolares nem de saúde dos jovens, para cumprir a LGPD e o ECA.

**Critério de aceite**
- Dado que estou logado(a) como Captação, quando eu abrir um jovem, então os campos de nível e frequência escolar, acompanhamentos e saúde não aparecem, nem em relatórios.
- Dado que estou logado(a) como Coordenador(a), então vejo esses campos para os jovens do meu núcleo.

**Nota técnica:** Field-Level Security via `MTB_Captacao`; sem acesso de objeto a `Acompanhamento_Escolar__c`.
**Fase:** 1 · **Prioridade:** Must

### US35 — Validações de qualidade nos dados do jovem
**História:** Como Admin, quero que o sistema impeça cadastros inconsistentes de jovens, para que os KPIs sejam confiáveis.

**Critério de aceite**
- Um Contact Jovem sem núcleo não pode ser salvo.
- Uma data de saída anterior à data de ingresso não pode ser salva.
- Um jovem com nível Superior em curso ou Superior completo e sem curso superior preenchido não pode ser salvo.
- Cada bloqueio mostra uma mensagem em português explicando como corrigir.

**Nota técnica:** Validation Rules no Contact (Record Type Jovem).
**Fase:** 1 · **Prioridade:** Must

---

## Requisitos não funcionais

| ID | Requisito | Como verificar |
| --- | --- | --- |
| RNF01 | Somente dados 100% fictícios na org e no repositório (beneficiários menores: LGPD e ECA) | Aviso no README; CSVs gerados por Mockaroo ou script |
| RNF02 | Volume de dados dentro do limite de 5 MB da Developer org | *Storage Usage* no Setup abaixo de 80% |
| RNF03 | Limiares de negócio (75%, 30 dias, R$ 2 mil, R$ 10 mil) parametrizados, sem valores fixos em Flow ou Apex | Alterar um registro de `MTB_Parametro__mdt` muda o comportamento |
| RNF04 | Todo Flow que grava dados tem fault path | Revisão de cada Flow no catálogo `docs/automacoes.md` |
| RNF05 | Código Apex com cobertura de testes acima de 85% e testes em lote (200 registros) | `sf apex run test --code-coverage` |
| RNF06 | Toda metadata versionada no GitHub, com validação de deploy e testes a cada push | GitHub Actions verde |
| RNF07 | Projeto reproduzível do zero em uma org nova | `scripts/setup.sh` sobe metadata e dados sem passos manuais além do NPSP |
| RNF08 | Convenções de nomes: API em português sem acento, labels com acento, prefixo `MTB_` e *Description* preenchida em todo objeto, campo e Flow | Revisão antes de fechar cada fase |

---

## Decisões em aberto

| Tema | Proposta | Onde registrar |
| --- | --- | --- |
| Duas automações para risco de evasão (US23) | Flow na Fase 3; desativar quando o Batch entrar na Fase 5 | ADR 003 |
| Atualização da etapa da trilha pela certificação (US22) | Novo Record-Triggered Flow `MTB_Atualiza_Etapa_Trilha`, fora do catálogo original | Catálogo de automações |
| Instrutor com ou sem login (US20, US24) | Sem login: a chamada é feita pelo(a) coordenador(a); evita consumir licença | ADR ou nota em `docs/seguranca.md` |
| V4S ou objeto próprio para turnos (US32) | V4S, se instalar sem conflito com o NPSP | ADR na Fase 6 |
| Visibilidade de `Despesa__c` | OWD Private + Sharing Rule por núcleo, como os jovens | `docs/seguranca.md` |
| Campos de saúde (US34) | O modelo de dados não define nenhum; criar 1 ou 2 campos (ex.: restrições médicas) ou remover "saúde" do critério | Modelo de dados / ERD |
