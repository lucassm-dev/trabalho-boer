# Design — Parte do Lucas (slides 04–07 → 10 slides)

Data: 2026-09-30 · Status: implementado em 2026-09-30.
Arquivo afetado: `apresentacao-gestao-agricola.html` (e `roteiro-video.md`, `PRODUCT.md`).

## 1. Objetivo

Hoje a parte do Lucas tem 4 slides (O problema · Finalidade e objetivos · Funcionalidades ·
Usuários e arquitetura, `data-slide` 3–6). A ideia é trocar esses 4 por **10 slides** mais ricos e
dinâmicos, para que a própria apresentação guie a fala: conteúdo revelado por etapas, um exemplo
contado como história, mockups de tela, diagramas UML e uma única animação.

**Sucesso:** o Lucas consegue explicar cada slide seguindo o que aparece a cada clique, sem
depender de decorar texto, e os requisitos do professor (finalidade, objetivos, funcionalidades)
continuam explícitos.

## 2. Restrições

- Arquivo HTML único e autocontido. Imagens em SVG/HTML inline, sem recursos externos novos.
- Manter o estilo visual atual: Outfit + Inter, paleta clara, acento laranja + verde-petróleo da
  UNIFEF, as classes e os layouts existentes sempre que possível.
- **O escopo do sistema não muda.** Tudo o que for mostrado precisa existir no cronograma do
  Monday.com (7 fases, 53 atividades) que a Rhiady apresenta.
- Nada fora da parte do Lucas muda de conteúdo: capa, membros, transições e os slides da Rhiady
  ficam como estão. A contagem e a barra de progresso se ajustam sozinhas porque são calculadas
  pelo índice.
- Vídeo gravado em tela cheia 16:9. A navegação continua por ← → / espaço / botões.

## 3. A história: Seu Ricardo e "O Gerente"

O **Seu Ricardo é um exemplo**, e o sistema serve para pequenos e médios citricultores em geral. Os
textos precisam deixar isso claro (ex.: "o Seu Ricardo é um entre muitos produtores que…").

| Dado | Valor | Origem |
|---|---|---|
| Nome do sistema | **O Gerente**, apelido do Seu Ricardo (avô do Lucas) | real |
| Local | Urânia-SP | real |
| Área | 12 alqueires paulistas (~29 ha) | real |
| Cultura | só laranja | real |
| Venda | vende a fruta para quem vem fazer a colheita | real |
| Funcionário | **Luciano** (tio do Lucas) | real |
| Mão de obra extra | peões/diaristas na colheita e em alguns serviços → **custo de mão de obra (diárias)**, não é perfil de usuário | real |
| Resp. técnico | **Eng. agrônoma Carla** | fictício (etiquetado) |
| Talhões | 4 talhões de 3 alqueires: Talhão 1 – Sede, Talhão 2 – Córrego, Talhão 3 – Estrada, Talhão 4 – Fundo | fictício |
| Números financeiros e de colheita | ver slide 6 | fictício (plausível) |

**Dores reais** relatadas: gastos anotados no papel e muitos que nem são anotados (diesel, peças de
reposição de equipamentos danificados); faturamento da safra incerto; nenhum aviso de vencimento de
boletos.

**Decisão sobre boletos:** o aviso de vencimento **não entra no escopo**. Aparece só como
"Próximos passos" (slide 5).

Os mockups levam o selo **"protótipo ilustrativo"**, porque o projeto ainda é só escopo e não tem
tela nem código. A nota "história real · alguns dados ilustrativos" aparece no slide 1.

## 4. Mecânica de interação

### 4.1 Revelação por etapas (aplicada em todos os 10 slides)
- Os elementos marcados com `data-step="n"` começam ocultos no slide.
- **→ / espaço / Próximo:** revela o próximo passo do slide atual. Quando não há mais passos,
  avança para o próximo slide.
- **← / Anterior:** oculta o último passo revelado. Quando nenhum passo está revelado, volta para o
  slide anterior.
- Quem **volta** para um slide vindo do seguinte encontra todos os passos já revelados, sem
  precisar repetir.
- Transição sempre igual e discreta: fade + leve subida (~300 ms). Nada de efeitos variados.
- Com `prefers-reduced-motion`, a revelação acontece sem movimento.

### 4.2 Animação (usada só no slide 10)
- Mensagens do diagrama de sequência desenhadas com `stroke-dashoffset`: a seta "percorre" o
  caminho e o rótulo aparece em seguida.

## 5. Os 10 slides

Cada slide tem `data-speaker="Lucas Mendes"` e um `data-topic`.

### 1 · Conheça o Seu Ricardo
- Título: *"Este é o Seu Ricardo. Na família, ele é o Gerente."*
- Subtítulo: ele é um entre muitos pequenos e médios citricultores da região.
- Ilustração SVG do sítio visto de cima: 4 talhões com fileiras de laranjeiras, a sede e o córrego.
- **Passo 1:** chips *Urânia-SP · 12 alqueires (~29 ha) · só laranja · vende para quem vem colher*.
- **Passo 2:** as pessoas: Seu Ricardo (produtor) · Luciano (funcionário) · Carla (resp. técnica,
  fictícia) · diaristas na colheita.
- Nota: "história real · alguns dados ilustrativos".

### 2 · O problema
- Título atual mantido: *"A gestão do sítio ainda vive no caderno."*
- Uma dor por passo, cada uma com o exemplo do sítio:
  1. **Gastos que escapam** (selo *real*): o diesel da semana e a peça do trator quebrado nunca
     entram no caderno.
  2. **Faturamento incerto** (selo *real*): no fim da safra, não se sabe ao certo quanto rendeu.
  3. **Estoque sem controle:** adubo comprado de novo porque ninguém lembrava que tinha no galpão.
  4. **Aplicações sem histórico:** qual talhão recebeu defensivo, e quando?

### 3 · Antes × depois
- **Esquerda (visível):** ilustração SVG de caderno bagunçado, com rabiscos, "diesel ???", conta
  riscada e folha solta.
- **Passo 1:** à direita, mini-tela do O Gerente com os mesmos gastos organizados por categoria e
  com total.
- Frase: *"Mesma informação, agora com controle."*

### 4 · "O Gerente": finalidade e objetivos
- Abertura: *"O sistema leva o apelido do Seu Ricardo, mas foi pensado para qualquer pequeno ou
  médio citricultor."*
- Finalidade (texto atual): centralizar a gestão da propriedade citrícola em um sistema web simples,
  do plantio à colheita.
- Seis objetivos em 3 passos (2 por passo), usando a lista atual. O objetivo 5 passa a ser:
  *"Acompanhar **custos (incluindo diesel, manutenção e diárias) e o faturamento** de cada safra"*.

### 5 · Funcionalidades
- Os 8 módulos atuais, cada um com uma linha de exemplo:
  - **Passo 1, no campo:** Propriedades e talhões ("os 4 talhões do sítio cadastrados") ·
    Culturas e atividades ("Luciano registra a adubação do Talhão 2") · Estoque e insumos
    ("entrada de 10 sacos de adubo") · Aplicações e ocorrências ("Carla registra o greening
    encontrado no Talhão 3").
  - **Passo 2, na gestão:** Colheitas e custos ("diesel, peças e diárias lançados na safra") ·
    Dashboard e relatórios ("quanto a safra rendeu") · Autenticação e perfis ("cada um vê o que
    precisa") · Regras de negócio ("não aplica o que não tem em estoque").
- **Passo 3:** card tracejado **Próximos passos: aviso de vencimento de boletos**.

### 6 · Mockup: dashboard
- Moldura de tela com o selo "protótipo ilustrativo". Cabeçalho: "O Gerente · Safra 2026/27 ·
  Olá, Ricardo".
- **Passo 1, custo × faturamento:** Faturamento R$ 684.000 (18.000 cx × R$ 38/cx) · Custos
  R$ 498.300 · Saldo **R$ 185.700**.
- **Passo 2, gastos por categoria** (barras horizontais): Adubos e insumos R$ 168.000 · Defensivos
  R$ 142.500 · Mão de obra/diárias R$ 96.800 · Diesel R$ 52.400 · Manutenção/peças R$ 38.600.
- **Passo 3, colheita por talhão (caixas):** T1 Sede 5.200 · T2 Córrego 4.300 · T3 Estrada 3.900
  · T4 Fundo 4.600 (total 18.000).
- **Passo 4, alertas:** "Estoque baixo: fungicida cúprico (20 L)" · "Aplicação pendente: Talhão 3".
- Os valores são fictícios e a nota fica visível no rodapé do mockup.

### 7 · Mockup: aplicação bloqueada
- Tela "Registrar aplicação", preenchida: Responsável Luciano · Talhão 2 – Córrego · Produto
  fungicida cúprico · Quantidade 40 L · Data.
- **Passo 1:** botão "Salvar" em estado pressionado e alerta **"Saldo insuficiente: há 20 L em
  estoque."**
- Legenda: *"A regra fica no backend: o sistema não deixa registrar o que não existe no galpão."*
- Serve de ponte para o slide 10 (mesmo cenário).

### 8 · UML: casos de uso
- Fronteira do sistema "O Gerente". Atores à esquerda (bonecos UML).
- **Passo 1, Produtor:** Cadastrar propriedade e talhões · Lançar custos · Consultar dashboard ·
  Gerar relatórios · Gerenciar usuários.
- **Passo 2, Funcionário:** Registrar atividade · Registrar colheita · Movimentar estoque ·
  Registrar aplicação.
- **Passo 3, Resp. técnico:** Registrar aplicação · Registrar ocorrência fitossanitária.
- **Passo 4:** `«include»` de "Registrar aplicação" para **"Validar saldo de estoque"**.

### 9 · UML: classes
- 9 classes com os atributos principais e as multiplicidades:
  - **Passo 1, estrutura:** `Propriedade` (nome, municipio, areaAlqueires) 1—* `Talhao`
    (nome, area) 1—* `Cultura` (variedade, anoPlantio).
  - **Passo 2, operação:** `Atividade` (tipo, data) * —1 Talhao · `Aplicacao` (data, quantidade)
    * —1 Talhao, * —1 `Insumo` (nome, unidade, **saldo**).
  - **Passo 3, gestão:** `Colheita` (data, caixas, precoCaixa) * —1 Talhao · `Custo` (data, valor,
    **categoria**: insumo | defensivo | diesel | manutencao | maoDeObra) · `Usuario` (nome,
    **perfil**: PRODUTOR | FUNCIONARIO | RESP_TECNICO), responsável por Atividade/Aplicacao.
- `Custo` em destaque com a cor de acento.

### 10 · Arquitetura + sequência (única animação)
- **Coluna esquerda, compacta:** camadas Angular → REST/JSON → Controller · Service · Repository →
  PostgreSQL, dentro de "Docker". Abaixo, as tags: Angular, Spring Boot, API REST, PostgreSQL,
  Docker, Figma, JUnit + Mockito, Postman, UML.
- **Direita, diagrama de sequência** com as linhas de vida: Luciano · Tela (Angular) ·
  AplicacaoController · AplicacaoService · InsumoRepository · PostgreSQL.
- 5 passos, cada um desenhando suas mensagens:
  1. Luciano → Tela: salvar · Tela → Controller: `POST /api/aplicacoes`
  2. Controller → Service: `registrar(dto)`
  3. Service → Repository: `buscarSaldo(insumoId)` · Repository → PostgreSQL: `SELECT saldo` ·
     retorno `20 L`
  4. Service: `[20 < 40]` lança `SaldoInsuficienteException` (fragmento `alt`)
  5. Controller → Tela: `422 Saldo insuficiente` · Tela → Luciano: alerta
- A camada da esquerda correspondente acende junto com cada passo.
- Fecha passando para a transição da Rhiady.

## 6. Demais arquivos

- **`roteiro-video.md`:** reescrever a Parte 1 com uma fala curta por slide e por passo. A
  numeração dos slides da Rhiady no roteiro passa de 08–15 para 14–21 (só o número muda, o texto
  continua).
- **`PRODUCT.md`:** registrar o nome "O Gerente", a história do Seu Ricardo e a regra de que os
  dados fictícios são etiquetados.
- Capa e encerramento **não mudam** (decisão: "O Gerente" só na parte do Lucas).

## 7. Verificação

- Abrir no navegador em 1920×1080 e percorrer todos os passos com → e ←, conferindo a regra de
  voltar para um slide com os passos já revelados.
- Conferir o slide 2 (transição de membros) e todos os slides da Rhiady: nada pode quebrar
  (simulação de atraso, Gantt).
- Checar que nenhum texto fica cortado ou sobreposto em 1366×768.
- Conferir `prefers-reduced-motion`.

## 8. Fora de escopo

- Módulo financeiro / contas a pagar / aviso de boletos (só "próximos passos").
- Perfil de usuário para diaristas.
- Mudanças na capa, no encerramento e nos slides da Rhiady.
