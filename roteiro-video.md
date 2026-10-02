# Roteiro do vídeo — Sistema de Gestão Agrícola Cítrica

Abrir `apresentacao-gestao-agricola.html` no navegador em tela cheia (F11). Navegar com ← →.
Tempo estimado: 11 a 13 minutos.

---

## Abertura (Lucas)

**01 · Capa**
"Olá, professor Marcelo e turma. Somos Lucas Mendes e Rhiady Vieira, do 6º semestre de Sistemas de
Informação da UNIFEF. Vamos apresentar o Sistema de Gestão Agrícola para Pequenos e Médios Produtores
de Frutas Cítricas, projeto que planejamos na última atividade da AV1."

**02 · Quem apresenta cada parte**
"Eu apresento o projeto: o Seu Ricardo, o problema, os objetivos, as funcionalidades, os protótipos,
a UML e a arquitetura. A Rhiady apresenta o planejamento: o cronograma no Monday.com, a análise e a
simulação de atraso."

## Parte 1 — O projeto (Lucas)

> Os slides desta parte revelam o conteúdo **por etapas**: cada → mostra o próximo bloco, e só
> depois do último bloco o → avança de slide. Os pontinhos laranja no rodapé mostram quantas etapas
> faltam. Voltar (←) esconde a última etapa; voltando de um slide seguinte, ele já aparece completo.

**03 · Transição** — só avançar.

**04 · Conheça o Seu Ricardo** (2 cliques)
"Para explicar o sistema, vamos usar um exemplo real: o Seu Ricardo, meu avô, citricultor em Urânia.
Na família, o apelido dele é *o Gerente*." — **→** "O sítio tem 12 alqueires, cerca de 29 hectares,
só de laranja, dividido em talhões. Ele vende a fruta no pé: quem compra vem colher." — **→** "Quem
trabalha ali: ele, que decide e paga as contas; o Luciano, meu tio, no dia a dia; uma agrônoma que
orienta as aplicações — aqui chamamos de Carla; e diaristas na colheita. Ele é um exemplo: o
sistema serve para qualquer pequeno ou médio produtor."

**05 · O problema** (4 cliques)
"E como é a gestão hoje? No caderno." — **→** "Primeiro, os gastos escapam: o diesel e a peça do
trator nem chegam a ser anotados." — **→** "Segundo, ele não sabe ao certo quanto a safra rendeu.
Essas duas são dores reais dele." — **→** "Terceiro, estoque sem controle." — **→** "E quarto,
nenhum histórico de quais talhões receberam defensivo."

**06 · Antes × depois** (1 clique)
"Esse é o caderno: valor com interrogação, diesel sem valor, e até um boleto que ele não lembra o dia."
— **→** "No sistema, a mesma informação vira lançamento com categoria, valor e total. O diesel e a
peça, que antes escapavam, agora aparecem."

**07 · O Gerente: finalidade e objetivos** (3 cliques)
"Por isso o sistema se chama O Gerente. A finalidade é centralizar a gestão da propriedade citrícola
em um sistema web simples, do plantio à colheita." — **→ → →** ler os objetivos de dois em dois,
destacando o 5: custos com diesel, manutenção e diárias, e o faturamento da safra.

**08 · Funcionalidades** (3 cliques)
"Esses objetivos viraram oito módulos." — **→** "No campo: talhões, atividades, estoque e
aplicações — cada um com um exemplo do sítio." — **→** "Na gestão: colheitas e custos, painel,
perfis de acesso e as regras de negócio." — **→** "E o aviso de boletos, que também é uma dor do Seu
Ricardo, fica registrado como próximo passo, fora do escopo desta versão."

**09 · Protótipo: painel** (4 cliques)
"Assim ficaria o painel do produtor. É um protótipo ilustrativo, com valores fictícios." — **→**
"Faturamento, custos e saldo da safra." — **→** "Os gastos por categoria, com diesel e peças em
destaque." — **→** "A colheita por talhão." — **→** "E os alertas: estoque baixo e aplicação
pendente."

**10 · Protótipo: regra de negócio** (1 clique)
"O Luciano vai registrar 40 litros de fungicida, mas só tem 20 no galpão." — **→** "O sistema
bloqueia: saldo insuficiente. Essa regra fica no backend. Vamos ver esse mesmo cenário por dentro
daqui a pouco."

**11 · UML: casos de uso** (4 cliques)
"Na modelagem, as pessoas do sítio viram atores." — **→** Produtor. — **→** Funcionário. — **→**
Responsável técnico. — **→** "E registrar aplicação sempre inclui validar o saldo de estoque."

**12 · UML: classes** (3 cliques)
"O que o sistema guarda:" — **→** "a estrutura: propriedade, talhão e cultura;" — **→** "a operação:
atividade, aplicação e insumo, com o saldo;" — **→** "e a gestão: colheita, usuário com perfil, e
custo com categoria — é aqui que o diesel e as peças deixam de escapar."

**13 · Arquitetura + sequência** (5 cliques — a única animação)
"A arquitetura é cliente-servidor: Angular, API REST, Spring Boot em Controller, Service e
Repository, e PostgreSQL, tudo em Docker. Vamos seguir aquela aplicação bloqueada." — **→** "O
Luciano salva; a tela faz um POST para a API." — **→** "O Controller chama o Service." — **→** "O
Service pede o saldo ao Repository, que consulta o banco: 20 litros." — **→** "20 é menor que 40:
o Service lança a exceção de saldo insuficiente." — **→** "O Controller devolve o erro 422 e a tela
mostra o alerta." — "Agora a Rhiady apresenta como planejamos tudo isso."

## Parte 2 — O planejamento (Rhiady)

**14 · Transição** — só avançar.

**15 · Como planejamos**
"Dividimos o projeto em 7 fases e 53 atividades, ao longo de 179 dias. No Monday.com, cada atividade
tem responsável, datas, duração, folga e dependência. A duração foi definida pela complexidade de
cada tarefa, e não um valor igual para todas."

**16 · Como ler uma atividade** (3 etapas)
"Antes do cronograma, um exemplo de como ler uma atividade: levantar necessidades dos usuários."
→ "A duração é de 4 dias úteis, de 22 a 25 de setembro." → "Ela depende de identificar os
stakeholders, então só começa depois dela." → "E tem 1 dia de folga: pode atrasar um dia sem empurrar
nenhuma outra atividade."

**17 · Cronograma**
"O projeto começa em 21 de setembro de 2026 e termina em 18 de março de 2027. A fase mais longa é a
Implementação, com 62 dias. Em laranja está a integração do frontend com a API, a atividade crítica
que vamos simular daqui a pouco."

**18 · Zoom por fase — CLICAR NAS FASES**
"Aqui dá para abrir cada fase e ver as atividades dela." Clicar em **Implementação**: "São 12
atividades. Em preto as do Lucas, em verde as minhas. À direita, a duração e a folga de cada uma."
Se quiser, clicar em mais uma fase (ex.: **Testes**) e avançar.

**19 · Quadro no Monday.com — DEMONSTRAÇÃO**
Clicar em **Abrir cronograma**. Mostrar: (1) o quadro principal com os grupos por fase, (2) as colunas
de folga e dependência, (3) a aba Gantt com as ligações. Voltar para a apresentação.
> Antes de gravar: confirmar que o link abre (logado ou com o quadro compartilhado).

**20 · Duas frentes em paralelo** (3 etapas)
"Na implementação o trabalho foi dividido em duas frentes. O Lucas faz o backend, um módulo depois do
outro." → "Ao mesmo tempo eu desenvolvo o frontend." → "As duas frentes se encontram na integração,
de 6 a 12 de janeiro, que só começa quando o backend termina." → "No projeto todo, são 31 atividades
do Lucas, 19 minhas e 3 em dupla."

**21 · Onde o cronograma não tem margem** (3 etapas)
"Cada quadradinho é uma das 53 atividades." → "Em verde, as 19 que têm folga, de 1 a 3 dias." →
"Em laranja, as 34 com folga zero: se atrasarem, o atraso passa adiante." → "Entre elas está a
integração do frontend com a API, que é também o ponto de encontro das duas frentes."

**22 · Análise do cronograma**
"Resumindo a análise: a primeira atividade é identificar os stakeholders, e a última antes da
manutenção é liberar a implantação piloto, em 4 de março. Backend e frontend foram planejados em
paralelo. As dependências seguem a ordem requisitos, análise, design, implementação, testes e
implantação. As folgas vão de 1 a 3 dias. A maior atividade é o dashboard, colheitas, custos e
relatórios, com 9 dias. E a que mais impacta se atrasar é a integração do frontend com a API REST,
que tem folga zero."

**23 · Simulação de atraso**
"Escolhemos essa integração, prevista de 6 a 12 de janeiro, e aplicamos 5 dias de atraso."
Clicar em **Aplicar atraso**. "Os testes que dependem dela foram empurrados, mas os testes funcionais
do frontend tinham folga e não mudaram. No fim, os testes terminam só 1 dia depois, e a implantação
piloto continua em 4 de março."

**24 · Como reduzir o impacto e o que aprendemos**
Ler as cinco ações de mitigação. Fechar com: "Nem todo atraso de 5 dias vira 5 dias no prazo final:
dependências, folgas e paralelismo permitem decidir antes que um atraso local vire um atraso global."

**25 · Encerramento** (os dois)
"Obrigado pela atenção!"
