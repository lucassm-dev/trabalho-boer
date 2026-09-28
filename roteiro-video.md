# Roteiro do vídeo — Sistema de Gestão Agrícola Cítrica

Abrir `apresentacao-gestao-agricola.html` no navegador em tela cheia (F11). Navegar com ← →.
Tempo estimado: 8 a 10 minutos.

---

## Abertura (Lucas)

**01 · Capa**
"Olá, professor Marcelo e turma. Somos Lucas Mendes e Rhiady Vieira, do 6º semestre de Sistemas de
Informação da UNIFEF. Vamos apresentar o Sistema de Gestão Agrícola para Pequenos e Médios Produtores
de Frutas Cítricas, projeto que planejamos na última atividade da AV1."

**02 · Quem apresenta cada parte**
"Eu apresento o projeto: o problema, os objetivos, as funcionalidades e a arquitetura. A Rhiady
apresenta o planejamento: o cronograma no Monday.com, a análise e a simulação de atraso."

## Parte 1 — O projeto (Lucas)

**03 · Transição** — só avançar.

**04 · O problema**
"Muitos pequenos e médios citricultores ainda controlam o pomar em caderno e planilha. Isso espalha
a informação dos talhões, deixa o estoque de insumos sem controle, não gera histórico das aplicações
de defensivos e dificulta saber quanto custou cada safra."

**05 · Finalidade e objetivos**
"A finalidade do sistema é centralizar a gestão da propriedade citrícola em um sistema web simples,
do plantio à colheita." Ler os seis objetivos rapidamente.

**06 · Funcionalidades**
"Esses objetivos viraram oito módulos." Citar cada um com uma frase. Destacar a validação de saldo no
estoque e o controle de acesso por perfil.

**07 · Usuários e arquitetura**
"São três perfis: produtor, funcionário e responsável técnico. A arquitetura é cliente-servidor: o
frontend em Angular conversa por uma API REST com o backend em Spring Boot, organizado em Controller,
Service e Repository, que grava no PostgreSQL. Tudo roda em containers Docker. O design foi feito no
Figma e a modelagem em UML." — "Agora a Rhiady apresenta como planejamos tudo isso."

## Parte 2 — O planejamento (Rhiady)

**08 · Transição** — só avançar.

**09 · Como planejamos**
"Dividimos o projeto em 7 fases e 53 atividades, ao longo de 179 dias. No Monday.com, cada atividade
tem responsável, datas, duração, folga e dependência. A duração foi definida pela complexidade de
cada tarefa, e não um valor igual para todas."

**10 · Cronograma**
"O projeto começa em 21 de setembro de 2026 e termina em 18 de março de 2027. A fase mais longa é a
Implementação, com 62 dias. Em laranja está a integração do frontend com a API, a atividade crítica
que vamos simular daqui a pouco."

**11 · Quadro no Monday.com — DEMONSTRAÇÃO**
Clicar em **Abrir cronograma**. Mostrar: (1) o quadro principal com os grupos por fase, (2) as colunas
de folga e dependência, (3) a aba Gantt com as ligações. Voltar para a apresentação.
> Antes de gravar: confirmar que o link abre (logado ou com o quadro compartilhado).

**12 · Análise do cronograma**
"A primeira atividade é identificar os stakeholders, e a última antes da manutenção é liberar a
implantação piloto, em 4 de março. Backend e frontend foram planejados em paralelo. As dependências
seguem a ordem requisitos, análise, design, implementação, testes e implantação. As folgas vão de 1 a
3 dias. A maior atividade é o dashboard, colheitas, custos e relatórios, com 9 dias. E a que mais
impacta se atrasar é a integração do frontend com a API REST, que tem folga zero."

**13 · Simulação de atraso**
"Escolhemos essa integração, prevista de 6 a 12 de janeiro, e aplicamos 5 dias de atraso."
Clicar em **Aplicar atraso**. "Os testes que dependem dela foram empurrados, mas os testes funcionais
do frontend tinham folga e não mudaram. No fim, os testes terminam só 1 dia depois, e a implantação
piloto continua em 4 de março."

**14 · Como reduzir o impacto e o que aprendemos**
Ler as cinco ações de mitigação. Fechar com: "Nem todo atraso de 5 dias vira 5 dias no prazo final:
dependências, folgas e paralelismo permitem decidir antes que um atraso local vire um atraso global."

**15 · Encerramento** (os dois)
"Obrigado pela atenção!"
